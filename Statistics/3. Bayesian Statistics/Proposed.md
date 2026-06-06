# Proposed Structure for `Statistics/3. Bayesian Statistics/`

Grounded in a full pass over STAT 238 (Berkeley, Spring 2026): 31 lecture PDFs and 11 labs read end-to-end. Replaces the earlier outline.

## Course Scope (Verified)

**Unit 1 — Foundations (L1–L7).** Bayes rule; prior, likelihood, posterior. Bayesian vs. frequentist reasoning and the likelihood principle (L2, L4). Credible intervals and the Student-$t$ posterior (L3). Hypothesis testing via Bayes factors and the Jeffreys-Lindley paradox (L5). Cox-Jaynes axiomatic derivation of probability from plausibility (L6-L7).

**Unit 2 — Conjugate Families (L8, L12-L14).** Beta distribution and Beta-Binomial conjugacy (L8). Dirichlet-Multinomial (L12). Bayesian bootstrap (L13). Evidence (marginal likelihood) maximization for hyperparameter learning, with digamma function (L14).

**Unit 3 — Hierarchical Models (L10-L11).** Kidney cancer Beta-Binomial hierarchy (L10). Normal hierarchical models with James-Stein shrinkage (L11). Empirical Bayes throughout. Delta method / variance stabilization (L10). (L9 file corrupted; content unknown.)

**Unit 4 — Bayesian Regression (L15-L17).** Bayesian linear regression with multivariate-$t$ posterior (L15). AutoRegression AR(1) as a likelihood-principle example (L16). Logistic regression with Laplace approximation + Newton's algorithm (L17).

**Unit 5 — Gaussian Processes (L19-L23).** High-dimensional regression with ReLU basis leading to GP prior (L19-L20). Brownian motion and integrated Brownian motion (L21). Gaussian processes with general kernels for interpolation, integration, regression (L22-L23). Sherman-Morrison-Woodbury for GP posterior inference (L23). (L18 file missing.)

**Unit 6 — MCMC (L24-L31).** Random Walk Metropolis (L24). Markov chain theory, stationary distribution, detailed balance, ergodic theorem, Metropolis-Hastings, Gibbs introduction (L25). Gibbs sampler applications: linear regression, probit via data augmentation, bivariate normal (L26-L27). Gibbs for mixture models (L28-L29) and k-component Gaussian mixtures (L30). EM algorithm as deterministic Gibbs analog (L30). MALA and Hamiltonian Monte Carlo (L31).

**NOT taught in STAT 238 (removed from earlier proposal):** variational inference, ELBO, ABC, Dirichlet processes, non-parametric Bayes. Any earlier version of this outline that included these was hallucinated.

## Proposed Folder Structure

Subfolders follow the README rule: 3+ notes or they get flattened.

```
Statistics/3. Bayesian Statistics/
├── 3. Bayesian Statistics.md                    (index)
│
├── 3.1 Bayesian Framework.md                    Prior, likelihood, posterior, Bayes' rule. Likelihood principle + stopping-rule invariance merged in.
├── 3.2 Credible Intervals.md                    Posterior-probability intervals vs. frequentist CIs.
├── 3.3 Bayes Factors.md                         Marginal likelihood ratio; Jeffreys-Lindley paradox.
├── 3.4 Cox-Jaynes Derivation.md                 Axiomatic derivation of probability from plausibility.
│
├── 3.5 Conjugate Families/
│   ├── 3.5 Conjugate Families.md                (index)
│   ├── 3.5.1 Beta-Binomial Model.md
│   ├── 3.5.2 Normal-Normal Model.md
│   ├── 3.5.3 Gamma-Poisson Model.md
│   └── 3.5.4 Dirichlet-Multinomial Model.md
│
├── 3.6 Hierarchical Models.md                   Two-level hierarchies; shrinkage; James-Stein; empirical Bayes.
├── 3.7 Marginal Likelihood.md                   Evidence, digamma, hyperparameter tuning.
├── [[1.5.2 Bayesian Bootstrap]]                 Already exists under 1. Statistical Inference / 1.5 Bootstrapping. Link from 3. index instead of duplicating.
│
├── 3.8 Bayesian Regression/
│   ├── 3.8 Bayesian Regression.md              (index)
│   ├── 3.8.1 Bayesian Linear Regression.md     Multivariate-t posterior.
│   ├── 3.8.2 Bayesian AutoRegression.md        AR(1); likelihood-principle implications.
│   ├── 3.8.3 Bayesian Logistic Regression.md   Laplace approximation; Newton's method.
│   └── 3.8.4 Bayesian Poisson Regression.md    Log-linear model; Laplace proposal for MCMC.
│
├── 3.9 Laplace Approximation.md                Gaussian posterior around MAP via Hessian.
│
├── 3.10 Gaussian Processes/
│   ├── 3.10 Gaussian Processes.md               (index)
│   ├── 3.10.1 Kernels.md                        RBF, linear, BM, IBM; kernel algebra.
│   ├── 3.10.2 GP Regression.md                  Posterior mean and variance; noise.
│   └── 3.10.3 Integrated Brownian Motion.md     Canonical GP used in the course.
│
└── 3.11 MCMC/
    ├── 3.11 MCMC.md                             (index: chain theory, ergodic theorem, diagnostics, tuning)
    ├── 3.11.1 Metropolis-Hastings.md            [EXISTING FULL NOTE]
    ├── 3.11.2 Gibbs Sampling.md                 Full conditionals; data augmentation as a property.
    ├── 3.11.3 MALA.md                           Langevin-adjusted proposal.
    ├── 3.11.4 Hamiltonian Monte Carlo.md        Leapfrog integration; momentum.
    └── 3.11.5 EM Algorithm.md                   Deterministic analog of Gibbs.
```

**Count:** 9 top-level notes + 4 subfolders (18 subnotes) + 4 subfolder indexes = 27 substantive notes total.

## Cross-Domain Links (notes that should reference notes in other folders)

- `3.4 Cox-Jaynes Derivation` should cross-link to `Mathematics/1. Discrete Mathematics/` (formal logic) and any existing measure-theoretic probability notes.
- `3.10.3 Integrated Brownian Motion` should link to `Mathematics/2. Probability/4. Stochastic Processes/4.6 Brownian Motion`.
- `3.11 MCMC` should link to `Mathematics/2. Probability/4. Stochastic Processes/4.33 Markov Chains/` for the prerequisite Markov-chain theory.
- `3.9 Laplace Approximation` should link to `Mathematics/9. Mathematical Optimization/` (Newton's method).
- Bayesian bootstrap content is hosted at `[[1.5.2 Bayesian Bootstrap]]` in `Statistics/1. Statistical Inference/1.5 Bootstrapping/`; the Bayesian Statistics folder links to it rather than duplicating.

## Priority Order for Writing Notes

Writing order reflects dependency: foundations first, then notes that other notes link into, then specialized topics. Starred notes are in the first batch.

1. ★ **3.1 Bayesian Framework** — foundational; every other note links here.
2. ★ **3.11 MCMC** (index) — parent for the MH note that already exists.
3. ★ **3.11.2 Gibbs Sampling** — currently a stub; blocks MH's "Relation to Gibbs" link.
4. **3.5.1 Beta-Binomial Model** — canonical conjugate example, referenced as the prototype.
5. **3.2 Credible Intervals** — cited in nearly every inference note.
6. **3.3 Bayes Factors** — stand-alone, high-value.
7. **3.9 Laplace Approximation** — used in the MH note's Poisson example.
8. **3.6 Hierarchical Models** — heavyweight single note incorporating James-Stein + empirical Bayes.
9. **3.5 Conjugate Families** (index + remaining three subfolders).
10. **3.10 Gaussian Processes** (index + three subfolders) — large block, done as a unit.
11. **3.8 Bayesian Regression** (index + four subfolders) — large block.
12. **3.11.3-3.11.5** — MALA, HMC, EM — written after the core MCMC notes are stable.
13. **3.4 Cox-Jaynes Derivation** — foundational but philosophical; lower reference weight.
14. **3.7 Marginal Likelihood** — rounds out Unit 2. Bayesian Bootstrap already exists at [[1.5.2 Bayesian Bootstrap]] — link, do not duplicate.
15. ~~Likelihood Principle~~ — folded directly into `3.1 Bayesian Framework`; does not need its own note.

## Notes to `_backlog/`

These appeared in the earlier proposal but are not taught in STAT 238. Moving them to backlog rather than deleting, since they may be taught in future courses (STAT 263, CS 281B, etc.):

- Variational Inference / ELBO / Mean-Field VI
- Approximate Bayesian Computation
- Dirichlet Processes and non-parametric Bayes

## Changes from Earlier Outline

- Removed: Variational Inference subfolder, ABC note, Non-Parametric Bayes subfolder.
- Added: Cox-Jaynes Derivation, Bayesian Bootstrap, Evidence/Marginal Likelihood, Laplace Approximation, Bayesian AutoRegression, Bayesian Logistic Regression, Bayesian Poisson Regression, EM Algorithm, MALA, HMC.
- Restructured: Conjugate Families promoted to subfolder (4 sub-notes). Bayesian Regression promoted to subfolder (4 sub-notes). Gaussian Processes includes IBM and Kernels as explicit sub-notes.
- MCMC placed last (now `3.11`), matching the course's ordering (MCMC in the final unit).
- Renumbered 2026-04-17 to close the gaps left by "3.2 Likelihood Principle" (folded into 3.1) and "3.9 Bayesian Bootstrap" (hosted externally at [[1.5.2 Bayesian Bootstrap]]). Sequence is now contiguous 3.1 through 3.11 with no missing numbers.

## Status

**Complete (2026-04-16):**
- [x] `3. Bayesian Statistics.md` — root index.
- [x] `3.1 Bayesian Framework.md` — includes Likelihood Principle.
- [x] `3.2 Credible Intervals.md`.
- [x] `3.3 Bayes Factors.md`.
- [x] `3.5 Conjugate Families/3.5 Conjugate Families.md` — subfolder index.
- [x] `3.5 Conjugate Families/3.5.1 Beta-Binomial Model.md`.
- [x] `3.5 Conjugate Families/3.5.2 Normal-Normal Model.md`.
- [x] `3.5 Conjugate Families/3.5.3 Gamma-Poisson Model.md`.
- [x] `3.5 Conjugate Families/3.5.4 Dirichlet-Multinomial Model.md`.
- [x] `3.6 Hierarchical Models.md` — James-Stein and empirical Bayes included.
- [x] `3.7 Marginal Likelihood.md` — evidence, digamma, BIC.
- [x] `3.8 Bayesian Regression/3.8 Bayesian Regression.md` — subfolder index.
- [x] `3.8 Bayesian Regression/3.8.1 Bayesian Linear Regression.md` — NIG conjugate, multivariate Student-t marginal, ridge/lasso as MAP.
- [x] `3.8 Bayesian Regression/3.8.2 Bayesian AutoRegression.md` — AR(1) as likelihood-principle illustration with stopping-rule invariance.
- [x] `3.8 Bayesian Regression/3.8.3 Bayesian Logistic Regression.md` — Laplace approximation, IRLS = Newton, MacKay's probit approximation.
- [x] `3.8 Bayesian Regression/3.8.4 Bayesian Poisson Regression.md` — log-linear model, Laplace-based MH proposal, overdispersion.
- [x] `3.9 Laplace Approximation.md`.
- [x] `3.10 Gaussian Processes/3.10 Gaussian Processes.md` — subfolder index.
- [x] `3.10 Gaussian Processes/3.10.1 Kernels.md` — kernel algebra, canonical kernels (BM, IBM, RBF, linear), Mercer decomposition.
- [x] `3.10 Gaussian Processes/3.10.2 GP Regression.md` — posterior formulas, Sherman-Morrison-Woodbury for flat linear priors, marginal likelihood.
- [x] `3.10 Gaussian Processes/3.10.3 Integrated Brownian Motion.md` — cubic-spline posterior mean, ReLU-basis limit.
- [x] `3.11 MCMC/3.11 MCMC.md` — subfolder index.
- [x] `3.11 MCMC/3.11.1 Metropolis-Hastings.md`.
- [x] `3.11 MCMC/3.11.2 Gibbs Sampling.md`.
- [x] `3.11 MCMC/3.11.3 MALA.md` — Langevin-drift proposal; drift $\tfrac{1}{2}\sigma^2 \nabla \log \pi$; mechanical (constant-acceleration) interpretation; optimal acceptance $\approx 0.574$.
- [x] `3.11 MCMC/3.11.4 Hamiltonian Monte Carlo.md` — augmented state $(x, p)$; leapfrog integrator; symplecticity and reversibility; NUTS adaptation; optimal acceptance $\approx 0.65$.
- [x] `3.11 MCMC/3.11.5 EM Algorithm.md` — deterministic analog of Gibbs; E-step computes responsibilities; M-step is weighted MLE; ELBO monotonic ascent; Gaussian-mixture and missing-data examples.
- [x] `3.4 Cox-Jaynes Derivation.md` — axiomatic derivation of probability from plausibility; product rule via associativity; sum rule via negation-consistency equation; $\mathbb{P} := w^\alpha$.

**Retrofitted prerequisites (outside the folder):**
- [x] `Mathematics/2. Probability/4. Stochastic Processes/4.33 Markov Chains/5.4 Reversibility.md` — fixed broken sentence, added frontmatter, Properties, Examples, cross-links to MCMC.
- [x] `Mathematics/2. Probability/4. Stochastic Processes/4.6 Brownian Motion.md` — full retrofit from empty stub: frontmatter, callout with four defining axioms, Properties (independent/Gaussian increments, covariance $\min(s,t)$, Markov, martingale, non-differentiability, quadratic variation, time-inversion self-similarity, reflection principle, Donsker construction), worked Examples, See Also linking to 3.12 GP notes.

**Pending:**
*(none)* — STAT 238 note coverage is complete as of 2026-04-16.

**Cross-references established:**
- Bayesian Bootstrap — hosted at [[1.5.2 Bayesian Bootstrap]] in `Statistics/1. Statistical Inference/1.5 Bootstrapping/`; linked from `3. Bayesian Statistics.md` rather than duplicated.
- Likelihood Principle — folded directly into `3.1 Bayesian Framework` with stopping-rule invariance treated as a Property.
