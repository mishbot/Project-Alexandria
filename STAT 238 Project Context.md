# STAT 238 Final Project — Context Primer for Claude Code

This document summarizes what's been discussed and decided about the project so far. Hand this to Claude Code at the start of a session so it has the right context.

## Project overview

**Title:** Bayesian Calibration of Stochastic Volatility Models via Flow-Augmented MCMC.

**Goal:** Implement and compare three Bayesian samplers for the stochastic volatility (SV) model on simulated data and real financial returns.

**The three samplers:**
1. **KSC mixture-of-normals Gibbs** — custom from-scratch implementation; the practitioner gold standard used as ground truth.
2. **NUTS** via PyMC — off-the-shelf strong baseline.
3. **Flow-augmented MCMC** — real-NVP normalizing flow trained online and used as MH proposal. Library: `flowMC` (JAX-based).

**Datasets:**
- Simulated SV process with known parameters (for posterior recovery checks).
- S&P 500 (`^GSPC`), 10-year daily window via `yfinance`.
- AAPL, same window, for generalization check.

**Comparison axes:**
- Mixing: ESS per second on marginals of $(\mu, \phi, \sigma_\eta)$ and on $h_{T/2}$.
- Posterior agreement: Wasserstein distance vs KSC as ground truth.
- Downstream accuracy: posterior-predictive 1-day and 10-day VaR forecasts, backtested with Kupiec test.

## The SV model

For daily log-returns $y_t$ over $T$ days:
$$y_t = e^{h_t/2}\,\varepsilon_t, \qquad h_t = \mu + \phi(h_{t-1} - \mu) + \sigma_\eta\,\eta_t,$$
with $\varepsilon_t, \eta_t \sim N(0, 1)$ i.i.d. and $h_0 \sim N(\mu, \sigma_\eta^2/(1 - \phi^2))$.

**Priors (weakly informative):**
- $\mu \sim N(0, 10^2)$
- $\phi \sim \text{Beta}(20, 1.5)$ to enforce near-unit-root stationarity
- $\sigma_\eta^{-2} \sim \text{Gamma}(2.5, 0.025)$

**Interpretation:**
- $h_t = \log \sigma_t^2$ (log-variance, not log-volatility).
- For SPX daily returns, typical $\mu \approx -9$ (~1% daily vol), $\phi \approx 0.97$, $\sigma_\eta \approx 0.15$.

## Project structure (7 steps)

1. **Data loading and preprocessing** — yfinance, compute log-returns, demean, sanity plots.
2. **Simulated SV truth set** — generate $(y_{\text{sim}}, h_{\text{sim}})$ with known $\theta_{\text{true}}$.
3. **KSC Gibbs sampler** — mixture indicators, FFBS for latent path, conjugate updates for parameters.
4. **NUTS via PyMC** — full joint posterior over $(\mu, \phi, \sigma_\eta, h_{1:T})$.
5. **Flow-augmented MCMC** — flowMC with real-NVP and RWM, recommended to marginalize $h_{1:T}$ first.
6. **Comparison metrics** — ESS/sec, Wasserstein, VaR, Kupiec test.
7. **Writeup** — methods, posterior recovery results, comparison.

Full plan with substeps and imports is in `STAT 238 Project Plan.md` (already in this vault).

## Realistic timeline

90–150 hours if everything works, 150–250 if the flow training fights you. The flow-augmented sampler is the dominant risk. Strongly recommended to marginalize $h_{1:T}$ out via KSC's mixture trick so the flow only operates over the 3-dim $\theta$ rather than the full 2500-dim joint.

## Compute resources

For the flow training step, the user is considering Modal (modal.com) for A100 access. Pay-per-second, free $30/month credit covers most of this project. Develop locally on CPU, push only the flow training to Modal.

## Style preferences (important)

These are the user's coding and writing conventions. Follow them strictly:

### Code style
- **Match course code conventions** (Lab 12, HW6 patterns).
- Use `np.random.seed(SEED)` at the top of the notebook + `norm.rvs(size=...)` calls, not `rng = np.random.default_rng(...)`.
- **Functions take their own seed argument**: `def simulate_sv(T, ..., seed=42)`.
- Use `from scipy.stats import norm, uniform, invgamma` and `norm.rvs(...)`, `uniform.rvs(...)`.
- Sparse, informal comments. `# Gibbs!` style is fine but doesn't pile on.
- No type hints, no multi-line docstrings.
- F-strings with terse formatting: `f"ESS = {ess:.0f}"`.
- **No vertical alignment of `=` signs** across multiple lines.
- Crude but readable. Don't over-engineer.

### Writing style
- Concise and direct. No motivational preamble. No summary postamble.
- One short transitional phrase per step: "By Bayes' rule...", "Recognizing the kernel...".
- Math in `$...$` inline, `\[ ... \]` display. No `align*` unless multi-line is needed.
- Bold "**Solution.**" when not using a `solution` environment.
- For LaTeX solutions, wrap in `\begin{solution} ... \end{solution}`. No QED, no postamble.
- **No em dashes (—)**. Use commas, colons, periods, or parentheses. The user is firm on this.

### LaTeX conventions
- Sample means: `\bar{\theta}` (with braces).
- Sums: `\sum_{i=1}^n` (with explicit limits).
- For matplotlib mathtext, use `\mathrm` not `\text` (mathtext doesn't support `\text`).

## Decisions already made

- **`yf.download` over `yf.Tickers`** for data fetching.
- **`pip install nbstripout`** to strip output cells from notebook diffs.
- **Repo name on GitHub:** `flow-sv-mcmc` (lowercase, hyphens).
- **Compound subscripts for tickers** in plot labels: `y_{t,\mathrm{GSPC}}`, not `y_t^{\mathrm{GSPC}}` (avoids double superscript when squaring).
- **Demeaned log-returns notation:** `y_t` (matches the SV model directly), with prose note "throughout, $y_t$ denotes the demeaned log-returns."

## Code patterns established

### Simulation function
```python
def simulate_sv(T, mu, sigma_eta, phi, seed=42):
    rng = np.random.default_rng(seed)
    h = np.empty(T)
    eta = norm.rvs(size=T - 1, random_state=rng)
    eps = norm.rvs(size=T, random_state=rng)
    h[0] = norm.rvs(
        loc=mu,
        scale=np.sqrt(sigma_eta**2 / (1 - phi**2)),
        random_state=rng,
    )
    for t in range(1, T):
        h[t] = mu + phi * (h[t-1] - mu) + sigma_eta * eta[t-1]
    y = np.exp(h / 2) * eps
    return y, h
```

### Sanity plot helper (4-panel)
```python
def sanity_plots(y, title, var):
    fig, axes = plt.subplots(2, 2, figsize=(12, 6))
    # Panel 1: time series of y
    # Panel 2: histogram with Gaussian overlay
    # Panel 3: ACF of y (lags 1-50, should be near zero at positive lags)
    # Panel 4: ACF of y^2 (lags 1-50, should decay slowly = volatility clustering)
    # ...full code in notebook
```

### Top-of-notebook config block
```python
# --- Data ---
TICKERS = ["^GSPC", "AAPL"]
START_DATE = "2014-01-01"
END_DATE = "2024-01-01"

# --- Simulation truth ---
MU_TRUE = -9.0
PHI_TRUE = 0.97
SIGMA_ETA_TRUE = 0.15
T_SIM = 2500

# --- Priors ---
PRIOR_MU_VAR = 100.0
PRIOR_PHI_BETA = (20.0, 1.5)
PRIOR_SIGMA_ETA_GAMMA = (2.5, 0.025)

# --- Sampler settings ---
KSC_N_ITER = 10000
KSC_BURN = 2000
NUTS_DRAWS = 2000
NUTS_TUNE = 1000
NUTS_TARGET_ACCEPT = 0.95
FLOW_N_LAYERS = 6
FLOW_HIDDEN = 32

# --- Reproducibility ---
SEED = 42
np.random.seed(SEED)
```

## Current status

Step 1 (data loading) and Step 2 (simulated truth set) are in progress. The user is working on the sanity plots and verifying the simulation function runs correctly.

## Key references

- Kim, Shephard, Chib (1998). "Stochastic volatility: likelihood inference and comparison with ARCH models." *Review of Economic Studies* 65(3).
- Gabrié, Rotskoff, vanden-Eijnden (2022). "Adaptive Monte Carlo augmented with normalizing flows." *PNAS* 119(10).
- Hoffman & Gelman (2014). "The No-U-Turn Sampler." *JMLR* 15(1).

## Things to do next (suggested order)

1. Finish Step 1 sanity plots for SPX and AAPL; confirm both show volatility clustering.
2. Finish Step 2 sanity plots for simulated data; confirm the simulation function produces realistic-looking returns.
3. Implement KSC Gibbs (Step 3) on simulated data first, verify posterior recovery of $\theta_{\text{true}}$.
4. Implement KSC Gibbs on SPX and AAPL.
5. Run PyMC NUTS (Step 4) on all three datasets.
6. Tackle flow-augmented MCMC (Step 5), starting with marginalized version on simulated data.
7. Comparison metrics (Step 6).
8. Writeup (Step 7).
