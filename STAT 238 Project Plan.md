# STAT 238 Project Plan

Bayesian Calibration of Stochastic Volatility Models via Flow-Augmented MCMC.

Three samplers (KSC mixture-of-normals Gibbs, NUTS via PyMC, flow-augmented MCMC), compared on simulated data, S&P 500, and AAPL.

## Working order

Step 1 → Step 2 → Step 3 (on simulated data) → Step 3 (on real data) → Step 4 → Step 5 → Step 6 → Step 7.

Get KSC fully working on simulated data before touching anything else — once `theta_true` is recoverable, the other two samplers have a baseline to match.

---

## Step 1: Data acquisition and preprocessing

### Substeps

1. Download S&P 500 daily closes for a ten-year window via `yf.download("^GSPC", start, end)`.
2. Download AAPL daily closes for the same window.
3. Compute log-returns: `r = np.log(P).diff().dropna()` for both series.
4. Demean each series: `y = r - r.mean()`.
5. Sanity plots per series: time series of `y`, histogram, ACF of `y` and `y²` to confirm volatility clustering.
6. Save processed series to pickle/CSV for downstream reuse.

### yfinance call

```python
data = yf.download(
    ["^GSPC", "AAPL"],
    start="2014-01-01",
    end="2024-01-01",
    auto_adjust=True,
    progress=False,
)
close = data["Close"]
log_returns = np.log(close).diff().dropna()
y = log_returns - log_returns.mean()
```

### Imports

```python
import numpy as np
import pandas as pd
import yfinance as yf
import matplotlib.pyplot as plt
from statsmodels.tsa.stattools import acf
```

---

## Step 2: Simulated-data generation (truth set)

### Substeps

1. Fix true parameters: `mu_true`, `phi_true`, `sigma_eta_true` (e.g., `-9.0`, `0.97`, `0.15`).
2. Initialize `h_0 ~ N(mu, sigma_eta² / (1 - phi²))` (stationary draw).
3. Simulate AR(1) latent path: `h_t = mu + phi*(h_{t-1} - mu) + sigma_eta * eta_t`.
4. Simulate observations: `y_t = exp(h_t/2) * eps_t`.
5. Save `(y_sim, h_sim, theta_true)` — ground truth for posterior recovery checks.

### Imports

```python
import numpy as np
import matplotlib.pyplot as plt
```

---

## Step 3: KSC mixture-of-normals Gibbs sampler

### Substeps

1. Transform: `z_t = log(y_t² + offset)` to handle numerical zeros; then `z_t = h_t + log(eps_t²)`.
2. Hardcode KSC's 7-component normal mixture for `log chi²₁` (weights/means/variances from Table 4 of Kim-Shephard-Chib 1998).
3. Gibbs loop:
   - **Mixture indicators:** sample `s_t | h_t, z_t` independently for each `t = 1, ..., T`.
   - **Latent path:** forward-filter-backward-sample (FFBS) for `h_{1:T} | s, mu, phi, sigma_eta, z` — Kalman forward pass, then backward sample.
   - **mu:** Normal conjugate update given `h_{1:T}` and `phi, sigma_eta`.
   - **phi:** Beta prior on `(phi+1)/2` to enforce stationarity; conjugate-via-transform or Metropolis step.
   - **sigma_eta²:** Inverse-Gamma conjugate update.
4. Run on simulated data, verify all three parameters in 95% CI and `h_sim` recovered within bands.
5. Run on SPX and AAPL series.
6. Save samples for each dataset.

### Imports

```python
import numpy as np
from scipy.stats import norm, invgamma, beta
from scipy.linalg import solve_triangular
from numba import njit  # speedup for FFBS inner loops
```

---

## Step 4: NUTS via PyMC on the full joint posterior

### Substeps

1. Build PyMC model over `(mu, phi, sigma_eta, h_{1:T})`:
   - Priors: `mu ~ N(0, 10²)`, `phi ~ Beta(20, 1.5)` (transformed to stationarity), `sigma_eta⁻² ~ Gamma(2.5, 0.025)`.
   - Initial state: `h_0 ~ N(mu, sigma_eta² / (1 - phi²))`.
   - Transitions: `h_t | h_{t-1} ~ N(mu + phi*(h_{t-1} - mu), sigma_eta²)`.
   - Observations: `y_t ~ N(0, exp(h_t/2))`.
2. Sample with `pm.sample(2000, target_accept=0.95)` — volatility posteriors have funnel geometry so high `target_accept` matters.
3. Run on simulated, SPX, and AAPL series.
4. Extract InferenceData via arviz, save samples.
5. Diagnostics: `az.summary`, ESS, R-hat, divergence count.

### Imports

```python
import pymc as pm
import pytensor.tensor as pt
import arviz as az
import numpy as np
```

---

## Step 5: Flow-augmented MCMC (real-NVP trained online + MH proposal)

### Substeps

1. Define log-posterior as a JIT-compatible JAX callable over `(mu, phi, sigma_eta, h_{1:T})`.
2. Configure flowMC sampler:
   - Base RWM proposal for the burst phase.
   - Real-NVP flow with ~6 affine coupling layers, ~32 hidden units per layer.
   - Alternating schedule: RWM bursts → train flow on accumulated samples → independent-MH stage using the flow as proposal → repeat.
3. Implement on simulated data first; verify `theta_true` and `h_sim` recovery.
4. Run on SPX and AAPL series.
5. Save samples.

### Imports

```python
import jax
import jax.numpy as jnp
from flowMC.sampler.Sampler import Sampler
from flowMC.nfmodel.realNVP import RealNVP
from flowMC.proposal.Gaussian_random_walk import GaussianRandomWalk
```

---

## Step 6: Comparison metrics

### Substeps

1. **ESS per second:** time each sampler's wall-clock; compute ESS for marginals of `mu, phi, sigma_eta` and for the representative latent state `h_{T/2}`; divide by elapsed seconds.
2. **Wasserstein distance:** for each parameter, compute `wasserstein_distance(samples_KSC, samples_NUTS)` and `wasserstein_distance(samples_KSC, samples_flow)`, treating KSC as ground truth.
3. **VaR posterior predictive:**
   - For each posterior `theta` sample, simulate forward `h_{T+1}, ..., h_{T+10}` and corresponding `y_{T+1}, ..., y_{T+10}`.
   - Aggregate one-day return distribution; take `0.01` and `0.05` quantiles for 1-day VaR.
   - Aggregate ten-day cumulative loss distribution; take quantiles for 10-day VaR.
4. **Kupiec test:** for each sampler's VaR forecast series, count realized SPX exceedances vs expected; compute LR statistic and p-value.
5. Produce tables and figures comparing all three samplers along all three axes.

### Imports

```python
import numpy as np
from scipy.stats import wasserstein_distance, chi2
import arviz as az
import time
import matplotlib.pyplot as plt
```

---

## Step 7: Writeup

### Substeps

1. Intro: motivate SV calibration, hard latent-path posterior, flow-augmented MCMC as a recent ML approach with limited financial evaluation.
2. Methods: full state-space model spec; one paragraph per sampler.
3. Posterior recovery results on simulated data: table of `theta_true` vs posterior mean ± CI for each sampler.
4. SPX comparison: ESS-per-second bar chart, marginal posterior overlay plots, Wasserstein distance table, latent-path posterior bands for `h_t`.
5. AAPL comparison: same plots, confirming methodology generalizes beyond an index.
6. VaR results: posterior predictive VaR forecasts side-by-side, Kupiec test results.
7. Conclusion: when the flow helps, when it doesn't, scope for future work.

### Imports

```python
import matplotlib.pyplot as plt
```

---

## Full import header for the project notebook

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import yfinance as yf
import time

from scipy.stats import norm, invgamma, beta, wasserstein_distance, chi2
from scipy.special import logsumexp
from scipy.linalg import solve_triangular
from statsmodels.tsa.stattools import acf
from numba import njit

import pymc as pm
import pytensor.tensor as pt
import arviz as az

import jax
import jax.numpy as jnp
from flowMC.sampler.Sampler import Sampler
from flowMC.nfmodel.realNVP import RealNVP
from flowMC.proposal.Gaussian_random_walk import GaussianRandomWalk

from tqdm import tqdm

np.random.seed(42)
```

**Environment note:** PyMC and flowMC have heavy and conflicting dependencies (PyMC pulls PyTensor; flowMC pulls JAX). Install each in its own conda environment if version conflicts arise, and pickle intermediate samples between them.
