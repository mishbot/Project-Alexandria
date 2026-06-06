---
title: STAT 238 Lectures 25–37 Source Review
course: STAT 238
created: 2026-05-03
updated: 2026-05-03
tags:
  - domain/bayesian-statistics
  - type/index
  - level/intermediate
  - status/complete
---

A walkthrough of the second half of STAT 238 (Spring 2026, Guntuboyina) covering Markov chains, the Metropolis-Hastings family, Gibbs sampling and its applications, mixture-model fitting, MALA, Hamiltonian Monte Carlo, variational inference, and the EM algorithm. Each entry below summarizes one source file from `_sources/STAT 238/` so the vault has a navigable index of what was covered, what was coded, and what was practiced in lab.

# Lectures

## Lecture 25 — Markov Chains, Stationarity, Detailed Balance, MH and Gibbs (1 April 2026)

Sets up the entire MCMC unit. Defines time-homogeneous Markov chains via transition kernels $P(x,y)$ on discrete or continuous state spaces, defines stationary distributions as invariant measures of the kernel, and states the ergodic theorem (irreducibility plus stationarity gives almost-sure convergence of time averages to space averages). Introduces the detailed balance condition $\pi(y)P(y,x) = \pi(x)P(x,y)$ as a sufficient condition for stationarity, illustrated by a random walk on a graph with $\pi \propto \deg$. Derives the Metropolis-Hastings algorithm: given an arbitrary proposal kernel $Q(x,y)$, the acceptance probability $\min\{1, \pi(y)Q(y,x) / \pi(x)Q(x,y)\}$ produces a chain satisfying detailed balance with respect to $\pi$. Closes with the bivariate Gibbs sampler — alternately resampling $\theta_1$ and $\theta_2$ from their full conditionals — and a direct verification that it satisfies detailed balance.

## Lecture 26 — The Gibbs Sampler in General; Examples (3 April 2026)

Generalizes Gibbs to $\theta = (\Theta^{(1)}, \dots, \Theta^{(k)})$: at each step pick a coordinate $j$ uniformly and resample $\Theta^{(j)}$ from $p(\Theta^{(j)} \mid \Theta^{-(j)})$. Three illustrative examples: (i) bivariate normal $(\theta_1, \theta_2) \sim N(y, \begin{smallmatrix}1 & \rho\\ \rho & 1\end{smallmatrix})$ — used to expose the failure mode at $|\rho| \to 1$ where the chain freezes; (ii) Bayesian linear regression with the improper $1/\sigma$ prior, deriving the conjugate full conditionals $\beta \mid \sigma \sim N(\hat\beta, \sigma^2(X^TX)^{-1})$ and $1/\sigma^2 \mid \beta \sim \text{Gamma}(n/2,\, \|y - X\beta\|^2/2)$; (iii) probit regression with the uniform prior, where direct Gibbs on $\beta$ alone has no tractable conditional, motivating the data-augmentation trick using latent normals $w_i \sim N(x_i^T \beta, 1)$ with $y_i = \mathbb{1}\{w_i > 0\}$.

## Lecture 27 — Gibbs Sampler for Probit Regression (6 April 2026)

Develops the Albert-Chib data-augmentation Gibbs sampler for probit. Introduces latent $w = (w_1, \dots, w_n)$ with $w_i \mid \beta \sim N(x_i^T \beta, 1)$ and $y_i = \mathbb{1}\{w_i > 0\}$; shows that the joint posterior factors so that $\beta \mid w \sim N((X^TX)^{-1} X^T w,\, (X^TX)^{-1})$ and $w_i \mid \beta, y_i$ are independent truncated normals. Derives the inverse-CDF formula $w_i = x_i^T\beta + \Phi^{-1}((1-U)\Phi(a_0) + U\Phi(b_0))$ for sampling truncated $N(\mu, \sigma^2)$ on $(a, b)$, with $a, b$ chosen by the sign of $y_i$. Closes with the full algorithmic specification of the Gibbs sampler.

## Lecture 28 — Gibbs Sampler for Mixture Models (8 April 2026)

Introduces the augmentation Gibbs sampler for the two-component normal mixture $y_i \sim p N(\mu_1, 1) + (1-p) N(\mu_2, 1)$ with $p$ known. Reformulates the model with latent indicators $z_i \sim \text{Bernoulli}(p)$ and $y_i \mid z_i$ Gaussian to make the full conditionals tractable: $z_i \mid \mu, y$ is Bernoulli with success probability $p \phi(y_i, \mu_1, 1) / [p \phi(y_i, \mu_1, 1) + (1-p) \phi(y_i, \mu_2, 1)]$, and $\mu_j \mid z, y$ is normal with cluster-mean and cluster-size sufficient statistics (in the limit of an uninformative prior). Foreshadows the EM algorithm as a deterministic analog to be developed in the next lecture.

## Lecture 29 — Gibbs for Mixtures with Unknown Weight and Variances (10 April 2026)

Specifies the algorithm in full for the two-component case with known weight $w$ and known unit variance, and writes out the iteration step-by-step. Then generalizes the model to $y_i \sim (1-w) N(\mu_0, \sigma_0^2) + w N(\mu_1, \sigma_1^2)$ with all five parameters unknown, placing $w \sim \text{Beta}(a,b)$, $\mu_j \sim N(m, s^2)$, and $\sigma_j^2 \sim IG(\alpha, \beta)$ priors. Notes that this prior structure is conjugate so the full conditionals will all admit closed forms (formulae stated in Lecture 30), and warns that Gibbs convergence is sensitive to initialization because the log-likelihood is multimodal.

## Lecture 30 — Gibbs Sampler for $k$-Component Gaussian Mixtures and the EM Algorithm (13 April 2026)

States the full conditionals for the $k$-component model $y_i \sim \sum_{j=1}^k w_j N(\mu_j, \sigma_j^2)$ with Dirichlet, normal, and inverse-gamma priors:
- $z_i \mid w, \mu, \sigma, y \sim \text{Categorical}(r_{i1}, \dots, r_{ik})$ with responsibilities $r_{ij} = w_j \phi(y_i, \mu_j, \sigma_j^2) / \sum_\ell w_\ell \phi(y_i, \mu_\ell, \sigma_\ell^2)$.
- $w \mid z \sim \text{Dirichlet}(a_1 + n_1, \dots, a_k + n_k)$.
- $\mu_j \mid z, y, \sigma$ Gaussian with conjugate posterior mean and variance.
- $\sigma_j^2 \mid z, y, \mu \sim IG(\alpha + n_j/2, \beta + \tfrac{1}{2}\sum_{i:z_i=j}(y_i - \mu_j)^2)$.

Then derives the EM algorithm as a deterministic variant that replaces each Gibbs draw with its expectation: integer counts $n_j$ become soft counts $\sum_i r_{ij}$, the Dirichlet draw becomes the MAP weight $w_j = n_j / n$, and the conjugate means and variances become weighted MLEs. The connection between Gibbs and EM is laid out explicitly.

## Lecture 31 — RWM and the MALA Algorithm (15 April 2026)

Recaps Markov chain theory and Metropolis-Hastings, then introduces Random Walk Metropolis with proposal $y = x + \sigma z$, $z \sim N(0, I_d)$. Motivates the Metropolis-Adjusted Langevin Algorithm by adding a drift term $g(x)$ to the proposal and choosing $g$ to make the Metropolis-Hastings ratio nearly one for small steps. A first-order Taylor expansion of $\log[\pi(y) Q(y,x) / \pi(x) Q(x,y)]$ around $y = x$ forces $g(x) = (\sigma^2/2) \nabla \log \pi(x)$, giving the MALA proposal $y = x + (\sigma^2/2) \nabla \log \pi(x) + \sigma z$. Includes a beautiful mechanical interpretation: RWM is a free particle (constant velocity); MALA is a particle with constant acceleration $\nabla \log \pi(x)$ over the step interval $[0, \sigma]$; HMC (foreshadowed) is a particle with position-dependent acceleration.

## Lecture 32 — Dimension Scaling of RWM, MALA, and HMC (17 April 2026)

Quantitatively compares RWM, MALA, and HMC for the standard Gaussian target $\pi = N(0, I_d)$. For RWM, computes $\log[\pi(y)/\pi(x)] = -A$ with $\mathbb{E}[A] = d\sigma^2/2$ and $\text{std}(A) = O(\sigma\sqrt{d})$; concludes that the acceptance probability is non-degenerate iff $\sigma = O(d^{-1/2})$. Repeats the analysis for MALA, where the analogous quantity has expectation $O(\sigma^2)$ and standard deviation $O(\sigma^3 \sqrt{d})$, giving the MALA scaling $\sigma = O(d^{-1/6})$ — much larger than RWM's $d^{-1/2}$. Solves the HMC ODE exactly for the Gaussian: $y = x \cos\sigma + z \sin\sigma$, and shows that the Metropolis-Hastings ratio equals one identically — so HMC accepts with probability one for any $\sigma$. This is the punchline justifying HMC's use in high dimensions.

## Lecture 33 — Continuity Equation and Stationarity for HMC (20 April 2026)

Develops the theoretical machinery for proving stationarity of HMC. Restates the HMC ODE in first-order form $(\dot x, \dot v) = (v, \nabla \log \pi(x))$ and reformulates it via the Hamiltonian $H(x, v) = -\log \pi(x) + \tfrac{1}{2}\|v\|^2$ as $(\dot x, \dot v) = (\partial H / \partial v, -\partial H / \partial x)$. Verifies that $H$ is conserved along trajectories. Then states and proves the continuity equation: if $\dot S = V(t, S)$ and $S(0) \sim \rho_0$, then the density $\rho(t, \cdot)$ of $S(t, X)$ satisfies $\partial_t \rho = -\nabla \cdot (V \rho)$. Sets up the application to HMC for next lecture.

## Lecture 34 — Hamiltonian Dynamics, Symplecticity, and Leapfrog (22 April 2026)

Generalizes the Hamiltonian to $H(x, v) = -\log \pi(x) + K(v)$ for any symmetric kinetic energy $K$, with two examples: $K(v) = v^T M v / 2$ (preconditioned, Riemannian Manifold HMC) and $K(v) = \|v\|_1$ (non-second-order dynamics). Establishes three properties of the time-$\sigma$ flow $T_\sigma$:
- Reversibility: $T_\sigma^{-1} = S T_\sigma S$ where $S$ flips momentum.
- Hamiltonian conservation: $H(T_\sigma(x, v)) = H(x, v)$.
- Volume preservation: $\det J_{T_\sigma} = 1$ (proven by an infinitesimal Jacobian argument).

Introduces the leapfrog discretization with step $\epsilon$:
$$
v(t + \epsilon/2) = v(t) + (\epsilon/2)\nabla\log\pi(x(t)),\quad x(t+\epsilon) = x(t) + \epsilon v(t+\epsilon/2),\quad v(t+\epsilon) = v(t+\epsilon/2) + (\epsilon/2)\nabla\log\pi(x(t+\epsilon)).
$$
Shows that leapfrog preserves reversibility and volume but not the Hamiltonian (motivating the Metropolis correction next lecture). Proves stationarity of $\pi(x)\phi(v)$ under continuous Hamiltonian dynamics via the continuity equation: the divergence $\nabla \cdot (V \rho) = 0$ identically when $\rho = e^{-H} / Z$.

## Lecture 35 — HMC Algorithm and Detailed Balance Proof (24 April 2026)

Specifies the full HMC algorithm: sample $v \sim N(0, I_d)$, run $N = \sigma/\epsilon$ leapfrog steps to produce $(y, w)$, accept with probability $\min\{1, \exp(H(x, v) - H(y, w))\}$. Reformulates the deterministic-transition kernel $\Upsilon = S T_{\text{disc}, N}$ as an involution ($\Upsilon^2 = I$). Proves the general detailed-balance condition $\mathbb{P}\{(\Theta^{(t)}, V^{(t)}) \in A,\, (\Theta^{(t+1)}, V^{(t+1)}) \in B\} = \mathbb{P}\{\dots \in B,\, \dots \in A\}$ for the joint chain on $(x, v)$, exploiting the volume-preservation and involution properties of leapfrog. The proof shows why a velocity flip is necessary even though it does not affect the Hamiltonian, because it makes the deterministic update an involution.

## Lecture 36 — Variational Inference (27 April 2026)

Introduces variational inference as an alternative to MCMC. Sets up the optimization $\arg\min_{q \in Q} \text{KL}(q \| f_{\theta\mid y})$, derives the equivalent objective in terms of the Evidence Lower Bound (ELBO) $\text{ELBO}(q) = \int q(\theta) \log [f_{y, \theta}(y, \theta) / q(\theta)] d\theta$, and shows $\text{ELBO}(q) \le \log f_y(y)$ with equality at $q = f_{\theta\mid y}$. Provides the alternative decomposition $\text{ELBO}(q) = \mathbb{E}_q[\log f_{y\mid \theta}] - \text{KL}(q \| f_\theta)$.

Develops the worked example of Bayesian logistic regression with a Gaussian variational family $q = N(m, LL^T)$. Shows the ELBO becomes $\mathbb{E}_{\beta \sim N(m, LL^T)}[\ell(\beta)] + \sum_j \log L_{jj} + \tfrac{p}{2}(1 + \log 2\pi)$, with the entropy term coming from the Gaussian. Uses the reparameterization trick $\beta = m + Lz$ with $z \sim N(0, I_p)$ and Monte Carlo estimation to make the objective amenable to gradient ascent.

## Lecture 37 — VI Connection to EM and CAVI (29 April 2026)

Recaps the ELBO and proves the EM algorithm is a special case of variational inference. With model $f_{y, \theta \mid \alpha}$ and a hyperparameter $\alpha$ to be estimated by MLE, alternately maximizing $\text{ELBO}(q, \alpha)$ over $q$ (giving $q = f_{\theta \mid y, \alpha}$) and over $\alpha$ (giving the M-step). The objective $E(t, \alpha) = \int f_{\theta \mid y, \alpha^{(t)}}(\theta) \log f_{y, \theta \mid \alpha}(\theta) d\theta$ is exactly the EM auxiliary function.

Presents Coordinate Ascent Variational Inference (CAVI). With factorized variational family $q(\theta) = \prod_{j=1}^k q_j(\theta_j)$, the optimal $q_j^*$ satisfies $q_j^*(\theta_j) \propto \exp\{\int q_{-j}(\theta_{-j}) \log f_{\theta_j \mid y, \theta_{-j}}(\theta_j) d\theta_{-j}\}$. Two-step proof: first lemma minimizes $\int f \log(f/g)$ over densities $f$ to give $f^* \propto g$; second lemma generalizes to two factors.

# Code Notebooks

## CodeLecture 26 — Gibbs Sampler Examples

Walks through three Gibbs sampler implementations side-by-side. **Bivariate normal:** generates 100,000 samples for $(\theta_1, \theta_2) \sim N(0, \Sigma)$ with $\rho = 0.8$, plots the resulting scatter, trace plots, and marginal histograms; demonstrates the breakdown when $\rho = 0.9999$ (the chain barely moves). **Linear regression** on the Pearson father–son heights data (n = 1078): compares the Gibbs posterior for $(\beta_0, \beta_1, \sigma)$ against `statsmodels` OLS, verifies posterior marginals match the theoretical $t$, $t$, and $\chi^2$ distributions. **Probit regression:** sets up the frogs dataset (binary presence/absence at 212 sites) and fits both probit and logit GLMs as a baseline for the next lecture's data-augmentation Gibbs sampler.

## CodeLecture 27 — Gibbs for Probit + Mixture Models Setup

Implements the Albert-Chib data-augmentation Gibbs sampler for probit regression on the frogs dataset (8 covariates, n = 212). Compares 100,000 Gibbs iterations against the Laplace posterior normal approximation produced by `sm.GLM`; shows the two agree closely. Repeats on a small simulated dataset ($n = 15$, $\beta = (-4, 0.8)$) where the discrepancy is larger and uses dense grid integration to confirm the Gibbs sampler is closer to the true posterior than the Laplace approximation. Then transitions to mixture models: simulates $n = 500$ from a $0.7 N(0, 1) + 0.3 N(2.5, 1)$ mixture, plots the bimodal log-likelihood surface (with one spurious mode), and shows that EM, Gibbs, and small-step RWM can all get trapped at the spurious mode; large-step RWM ($\sigma = 1$) reliably escapes.

## CodeLecture 28 — Mixture EM and Gibbs (Sensitivity to Initialization)

Self-contained re-presentation of the mixture-model story from CodeLecture 27, repackaged for Lecture 28's content: same simulated data, same comparison of EM, Gibbs, and RWM, same demonstration that initialization matters and that large-step RWM is the most robust.

## CodeLecture 29 — Two-Component Mixture on the Exoplanet Dataset

Loads NASA's exoplanet archive (~6,000 planets, with planet radius in Jupiter radii on the log scale). Fits the two-component normal mixture using both PyMC (slow, ~80 seconds for 2,000 draws on 600-point subsample) and a custom Gibbs sampler (fast, 40,000 draws). Demonstrates label switching between the two methods (PyMC reports $w \approx 0.33$, Gibbs reports $w \approx 0.67$ — same fit, different labels). Shows the fitted bimodal density on the histogram. Concludes with a Gibbs run on the full ~6,000-point dataset, which PyMC cannot handle in reasonable time.

## CodeLecture 30 — k-Component Gaussian Mixture, Gibbs and EM

Generalizes the previous lecture's two-component sampler to arbitrary $k$. Reproduces the $k = 2$ result, then runs $k = 3$ on the exoplanet data, finding that the third component improves the fit by capturing a tail not modeled by two components; $k = 4$ does not visibly improve further. Uses the posterior modal assignments of $z_i$ to cluster the data into $k$ groups and visualize the per-component density contributions. Closes with the EM algorithm for $k$-component mixtures, showing that EM and Gibbs converge to similar fits when both are well-initialized.

## CodeLecture 31 — RWM in Low and High Dimensions

Implements RWM on the unnormalized 1D density $\sin^2(8.5\theta)\,e^\theta\,\mathbb{1}[0,1]$. With $\sigma = 0.3$, RWM produces excellent samples (good trace plot, fast-decaying autocorrelation). Then lifts the problem to $d = 5000$ by appending $X_2, \dots, X_d \sim N(0, 1)$, and shows that no value of $\sigma$ makes RWM work: too large an $\sigma$ gives near-zero acceptance, too small an $\sigma$ gives near-perfect autocorrelation. The dimension-scaling crisis demands MALA (next notebook).

## CodeLecture 32 — MALA in High Dimensions and Geometry of Proposals

Returns to the high-dimensional setup from CodeLecture 31 and shows that MALA produces good samples for the first coordinate where RWM fails. Includes a geometric visualization of how the three proposals look for $\pi = N(0, I_d)$: RWM is a straight-line proposal from $x$ in direction $z$; MALA is parabolic; HMC is even more curved (an ellipse arc). The visualization makes concrete why curved proposals work better in higher dimensions — they follow the geometry of the target.

## CodeLecture 35 — Leapfrog vs Euler; Bayesian Neural Network with HMC

Shows that leapfrog tracks the exact Hamiltonian flow accurately for $\pi = N(0, I_d)$ over $N = 200$ steps while Euler integration drifts away after a few steps. Then fits a Bayesian neural network with two hidden layers (20 units each, 661 parameters total) to the scikit-learn diabetes dataset using HMC. Tunes $\sigma$ via the SGD baseline residual std and $\tau$ via the SGD weight-decay parameter. Runs leapfrog with step size $\epsilon = 0.03$ and $L = 100$ steps to produce 1,000 samples. Test RMSE matches SGD baseline ($\sim 55$ on the original scale).

## CodeLecture 36 — Variational Inference for Bayesian Logistic Regression

Compares three approximations to Bayesian logistic regression posteriors: full-covariance Gaussian VI (reparameterization trick + Adam), Laplace approximation, and long-run RWM as ground truth. The 1D warm-up demonstrates that VI and Laplace both essentially nail the truth when the posterior is bell-shaped. The frogs dataset (8D, n = 212) shows where the approximations diverge: VI is faithful to the global KL; Laplace is a local quadratic approximation at the MAP. Builds the design matrix with log-transforms on `distance` and `NoOfPools` and standardizes covariates. The VI implementation maximizes the ELBO using PyTorch with Cholesky parameterization $\Sigma = LL^T$ to enforce positive-definiteness via gradient ascent on $L$.

# Labs

## Lab 6 — Linear Regression Mechanics

Walks through the OLS quantities reported by `statsmodels`, computing each by hand on the FRED quarterly US GDP series (n = 314) fit with a cubic time trend. Computes the design matrix $X$, the LSE $\hat\beta = (X^TX)^{-1}X^Ty$, fitted values, residuals, residual sum of squares (RSS), residual standard error $\hat\sigma = \sqrt{\text{RSS}/(n-4)}$, and standard errors of $\hat\beta$ as the square roots of the diagonal of $\hat\sigma^2(X^TX)^{-1}$. Verifies each quantity matches the corresponding `statsmodels` output. Closes by plotting $N = 200$ posterior samples of the regression curve drawn from the multivariate-$t$ posterior $\beta \mid \text{data} \sim t_{n-4, 4}(\hat\beta, \hat\sigma^2(X^TX)^{-1})$ to show the visual envelope of uncertainty.

## Lab 7 — Linear Regression on MROZ + Poisson Regression Introduction

Reviews linear regression on the MROZ dataset (n = 753, 22 covariates on married women in 1975) with `hours worked` as response and 11 covariates. Drops the variables with high $p$-values and refits with 6 covariates. Verifies that PyMC with `pm.Flat` priors on $\beta$ and $\log\sigma$ gives essentially identical posterior means and standard deviations to the OLS output. Then motivates Poisson regression as the right model for the count-valued response: the linear model's coefficient interpretations break down for $\text{kidslt6}$ (a $-430$-hour effect is meaningless for working women with hours $\ll 1000$ or hours $\gg 3000$), but a log-linear model gives the interpretable percentage interpretation. Fits the Poisson regression model via `sm.GLM`, derives the Newton-Raphson algorithm for the MLE explicitly (gradient $X^T(y - \mu)$, Hessian $-X^T M(\beta) X$), implements it in pure NumPy, and verifies convergence to the `statsmodels` answer. Compares the PyMC samples (with `pm.Flat` priors) against the frequentist output and shows that PyMC is unstable: random_seed = 0 works but random_seed = 4 fails to mix. Derives the Laplace posterior normal approximation from a second-order Taylor expansion of the log-likelihood at the MLE and shows that the resulting Bayesian standard errors coincide with the frequentist ones.

## Lab 8 — Bayesian Regularization and Trend Filtering

Fits the smoothing model $y_i = \theta_i + \epsilon_i$ with $\theta_i = \beta_0 + \beta_1(i-1) + \sum_{j=2}^{n-1} \beta_j (i-j)_+$ — i.e., a first-order trend filtering basis with one knot per data point. The full model is over-parameterized ($n-1$ knot coefficients plus an intercept and slope) and ridge regularization is necessary. Places a flat prior on $(\beta_0, \beta_1, \log\sigma)$ and a $N(0, \gamma^2 \sigma^2)$ prior on the knot coefficients. Derives the conditional posteriors of $\beta$, $\sigma$, and $\gamma$ in closed form and approximates the marginal posterior of $\gamma$ on a log-spaced grid. Generates posterior samples via this grid-based scheme and visualizes uncertainty bands around the smoothed estimate. Demonstrates on two datasets: a smooth function with $n = 1000$ (the method recovers the truth and the uncertainty bands cover the truth), and a piecewise-linear function with $n = 400$ (the method smooths over the kinks but recovers the overall shape).

## Lab 9 — Gaussian Process Regression with the RBF Kernel

Switches from the Integrated Brownian Motion (IBM) kernel used in the lectures to the squared exponential / RBF kernel $K(u, v) = \tau^2 \exp(-(u-v)^2 / 2\ell^2)$. Applies it to the wage dataset: $y = \log(\text{weekly wage})$ regressed on years of experience, with $n = 500$ subsampled from 25,437 records. Tunes the hyperparameters $(\tau^2, \ell, \sigma^2)$ first by grid search over the marginal likelihood, then by L-BFGS-B optimization for speed, and finally with an additional intercept parameter $\beta_0$. Compares the three RBF fits against the IBM-kernel result from Lecture 23 and finds they all give similar smooth fits. Demonstrates the qualitative effect of the length scale: $\ell \to \infty$ smooths the function flat, $\tau \to 0$ shrinks the function to zero.

## Lab 10 — Bayesian Approaches to Poisson Regression (MH Variants)

Returns to the MROZ Poisson regression from Lab 7. Compares four approaches:
1. **PyMC with random_seed = 0** — close to the frequentist answer.
2. **PyMC with random_seed = 4** — chain fails to mix.
3. **RWM with proposal covariance $\Sigma$ from the Laplace approximation** — works (acceptance ~25%, posterior matches Laplace).
4. **RWM with $\sigma^2 I$ proposal** — fails because the variables are on different scales.
5. **RWM with $\text{diag}(\Sigma)$ proposal** — works after burn-in.
6. **Independence sampler with proposal $N(\hat\beta, \rho \Sigma)$** for $\rho = 1.2$ — best mixing, ~80% acceptance, sensitive to initialization (must start at MLE).

The lab's takeaway is that the Laplace covariance is essential for tuning the proposal in non-Gaussian posteriors: it tells you the right scales for each direction of the posterior, and ignoring it gives you either a chain that takes too-small steps (high acceptance, no exploration) or one that takes too-large steps (low acceptance, no exploration).

## Lab 11 — Mixture of Regressions

Fits the mixture-of-regressions model $y_i = \beta_0^i + \beta_1^i x_i + \epsilon_i$ where $(\beta_0^i, \beta_1^i)$ is drawn from a 3-atom discrete distribution with unknown atoms and weights. Simulates $n = 400$ data points from three lines with coefficients $(3, -1)$, $(1, 1.5)$, $(-1, 0.5)$ at weights $(0.3, 0.3, 0.4)$. The Gibbs sampler proceeds: introduce latent indicators $z_i \in \{1, 2, 3\}$, alternately resample $z_i$ from $\text{Categorical}(p_{i1}, p_{i2}, p_{i3})$, weights $w$ from $\text{Dirichlet}(1 + n_1, 1 + n_2, 1 + n_3)$, and per-component coefficients $\gamma^j$ from their conjugate normal posterior. Recovers the true coefficients (up to label-switching), visualizes the posterior over regression lines as a band plot, and uses the posterior-mode assignments of $z_i$ to color-code the data points by component.

## Lab 12 — RWM, MALA, HMC Comparison on $\pi = N(0, I_d)$

Hands-on comparison of all three MCMC methods on the standard $d = 5000$ Gaussian using the dimension-scaling rules from Lecture 32. Implements all three samplers from scratch and computes diagnostics at each: (i) trace plot of the first coordinate; (ii) marginal histogram vs $N(0, 1)$; (iii) trace plot of $\|X\|^2 / d$ (target value 1); (iv) sample autocorrelation function; (v) effective sample size (ESS); (vi) running mean. **RWM at $\sigma = c/\sqrt d$:** acceptance $\sim 30\%$ but very poor mixing (ESS = 30 from 50,000 samples). **MALA at $\sigma = c d^{-1/6}$:** much better (ESS = 925), histogram matches the truth, $\|X\|^2 / d$ stabilizes near 1. **HMC with $\sigma = 0.5$:** acceptance is identically 1 (the exact-Gaussian solution can be evaluated in closed form), and ESS = 3,096 — best of the three by a factor of 3 over MALA. Confirms numerically the dimension-scaling theory of Lecture 32.

## Lab 13 — Bayesian Neural Network on Diabetes Data

Extends CodeLecture 35's BNN with HMC by adding a fully Bayesian treatment of $\sigma$ and $\tau$. First reproduces the fixed-$(\sigma, \tau)$ result, then constructs the posterior predictive distribution properly: draws $y_*^{(s)} \sim N(f_{\theta^{(s)}}(x_*), \sigma^2)$ for each posterior sample of $\theta$. Empirical 95% predictive coverage on the test set is 97.3% (well-calibrated), at the cost of intervals that are wide (average width 213, vs response std 77) — this is honest reporting of uncertainty given how few data points the BNN has. Then upgrades to the full hierarchical model with priors $\sigma^2 \sim IG(0.001, 0.001)$ and $\tau^2 \sim IG(0.001, 0.001)$. Implements Gibbs-within-HMC: HMC step on $\theta$ given $(\sigma, \tau)$, then closed-form inverse-gamma draws for $\sigma^2$ and $\tau^2$. The reasoning for this hybrid is that running HMC over the joint $(\theta, \log\sigma, \log\tau)$ requires a non-trivial mass matrix because the parameters live on different scales; Gibbs sidesteps this. Result: $\sigma$ posterior is well-pinned-down (matches the SGD value), but $\tau$ posterior is much broader than expected and the chain does not mix well — a known issue with hierarchical-model HMC, with references to Betancourt and Girolami (2013).

# What These Sources Add to the Vault

The lectures, code, and labs together extend the existing Bayesian-statistics notes in three ways. First, they provide concrete dimension-scaling theory ($d^{-1/2}$, $d^{-1/6}$, $d^{-1/4}$) for the three samplers and worked computations on $N(0, I_d)$ — material that lives in [[3.11.1 Metropolis-Hastings]], [[3.11.3 MALA]], and [[3.11.4 Hamiltonian Monte Carlo]]. Second, they give a complete derivation of HMC stationarity using the continuity equation, the involution structure, and the volume-preservation property of leapfrog — material that should be referenced from the HMC note. Third, they introduce variational inference and the connection to EM via the ELBO — material that is currently underdeveloped in the vault. A future note on variational inference (sitting alongside [[3.11.5 EM Algorithm]] in the MCMC/inference subfolder, or as a peer to the MCMC subfolder) would close this gap.

The labs also cover practical tooling that is not in the lectures: PyMC behavior and failures, posterior-predictive coverage diagnostics (autocorrelation, ESS, running means), the Cholesky parameterization for covariance optimization, and Gibbs-within-HMC for hierarchical models. These are good candidates for a separate "MCMC diagnostics" note or for being incorporated as Properties in the existing MCMC notes.

# See Also

- [[3.11 MCMC]] — parent index for the MCMC subfolder.
- [[3.11.1 Metropolis-Hastings]], [[3.11.2 Gibbs Sampling]], [[3.11.3 MALA]], [[3.11.4 Hamiltonian Monte Carlo]], [[3.11.5 EM Algorithm]] — concept notes that draw on this material.
- [[Proposed]] — the structural plan for the Bayesian Statistics folder, including notes on variational inference being deferred to `_backlog/`.
