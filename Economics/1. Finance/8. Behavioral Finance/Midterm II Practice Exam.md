---
title: Midterm II Practice Exam (Extended)
aliases: [Extended Practice Midterm II, Practice Exam II Extended]
course: ECON 138
lecture: [11, 12, 13, 14, 15, 16, 17, 18, 19]
created: 2026-04-08
updated: 2026-04-08
tags:
  - domain/finance
  - type/practice
  - level/intermediate
  - status/complete
prerequisites:
  - "[[8. Behavioral Finance]]"
---

>[!note] Midterm II Practice Exam (Extended)
>A deeper practice exam covering every topic from **Lectures $11$–$19$** of ECON 138, in the style and wording of the practice exam distributed by the staff on April 1, 2026. Each question is tagged with the **lecture** it draws from and the **topic class** — one of *Momentum / Reaction*, *Belief Biases*, *Bubbles & Limits to Arbitrage*, *Household Finance*, or *Prospect Theory*.
>
>**Total: $120$ points.** Sections: Multiple Choice ($30$), Short Questions ($40$), Long Question on BSV ($1998$) ($30$), Problem on Prospect Theory ($20$).
>
>Solutions are collapsed in `>[!example]-` blocks — attempt each question first, then expand.

# Section 1 — Multiple Choice ($30$ points)

*Each question is worth $5$ points.*

## Question 1

**(Lecture $17$–$18$ — Prospect Theory.)** Alice is offered two independent lotteries: (X) a $0.1\%$ chance of winning \$$10{,}000$ for a \$$5$ ticket, and (Y) a $0.1\%$ chance of losing \$$10{,}000$ which she can fully insure for a \$$15$ premium. Alice buys both the lottery ticket and the insurance. Which feature of prospect theory best rationalizes this combination of choices?

(a) Reference dependence — Alice evaluates both lotteries relative to her initial wealth and finds each attractive separately.
(b) Loss aversion — the kink at the origin makes Alice reject the lottery but accept the insurance.
(c) Probability weighting — Alice's weighting function $w(\cdot)$ overweights the low-probability events in both the gain domain and the loss domain.
(d) Diminishing sensitivity — the concave gain domain and convex loss domain pull in opposite directions but cancel out.

>[!example]- Answer
>**(c) Probability weighting.** Simultaneously buying lotteries and insurance is the canonical puzzle that Kahneman-Tversky's $w(\cdot)$ is designed to explain. Low-probability gains are overweighted (she overvalues the \$$10{,}000$ lottery payoff), and low-probability losses are also overweighted (she overvalues the tiny chance of losing \$$10{,}000$ and pays an unfairly-priced premium to hedge it). Loss aversion and diminishing sensitivity cannot produce both behaviors simultaneously; only probability reweighting can.

## Question 2

**(Lecture $12$ — Psychology of Preferences: Hyperbolic Discounting.)** Ben has quasi-hyperbolic preferences $(\beta, \delta)$ with $\beta = 0.6$. He signs up for a gym contract that charges him a $\$50$ penalty if he misses more than two workouts per month, even though the penalty-free alternative is cheaper. Which of the following best describes Ben?

(a) Ben is a naïf: he believes future-Ben will exercise, so he does not need a commitment device.
(b) Ben is a sophisticate: he correctly anticipates that future-Ben will procrastinate, and uses the penalty contract to bind future-Ben's behavior.
(c) Ben is exponentially patient: he values long-run health enough to willingly pay the penalty.
(d) Ben is loss averse: the \$$50$ penalty looms large in his mental accounting, causing him to exercise.

>[!example]- Answer
>**(b) Sophisticate.** The defining signature of a sophisticated hyperbolic discounter ([[8.10.6. Hyperbolic Discounting]], *O'Donoghue and Rabin*, $1999$) is the willing adoption of a commitment device — an action taken today that binds tomorrow's self. A naïf would reject the penalty contract because she believes her future self will follow through on its own. An exponential agent has no need for commitment because her preferences are time-consistent.

## Question 3

**(Lecture $14$ — Belief Biases.)** A stock has just announced earnings that miss analyst expectations by $5\%$. One group of investors ignores the news entirely and keeps their beliefs essentially unchanged, while another group extrapolates the miss into a sweeping "the company is in structural decline" narrative and revises their valuations sharply downward. In the Rabin ($1998$) parametric family of Bayes-rule distortions,
$$\frac{\pi(A \mid S)}{\pi(B \mid S)} = \left(\frac{p(S \mid A)}{p(S \mid B)}\right)^c \left(\frac{\pi(A)}{\pi(B)}\right)^d,$$
the two groups correspond to:

(a) The first group has $c < 1$ (conservatism); the second group has $c > 1$ (overreaction).
(b) The first group has $d > 1$ (confirmation bias); the second group has $d < 1$ (base-rate neglect).
(c) The first group has $c > 1$ (overreaction); the second group has $c < 1$ (conservatism).
(d) Both groups have $c = 1, d = 1$ but differ in their priors.

>[!example]- Answer
>**(a)** The first group *under-weights* the new signal — they hold the likelihood ratio below its Bayesian benchmark, which is $c < 1$ (conservatism, [[8.6.1. Conservatism]]). The second group *over-weights* the new signal, pushing the likelihood ratio above Bayesian, which is $c > 1$ (overreaction, [[8.6.2. Overreaction]]). The $d$ parameter governs base-rate weighting, not signal weighting.

## Question 4

**(Lecture $15$ — Bubbles and Limits to Arbitrage.)** Consider a one-period asset with payoff $\mu^{\text{true}}$ and volatility $\sigma$. Optimists believe the mean payoff is $\mu^{\text{true}} + \Delta$; pessimists believe it is $\mu^{\text{true}} - \Delta$. With unrestricted short-selling and equal wealth, the equilibrium price is $\mu^{\text{true}}/(1 + r)$. With a short-sale constraint, Miller ($1977$) shows the price becomes:

(a) $(\mu^{\text{true}} + \Delta - 2\theta\sigma^2)/(1 + r)$, strictly above the frictionless price.
(b) $(\mu^{\text{true}} - \Delta - 2\theta\sigma^2)/(1 + r)$, strictly below the frictionless price.
(c) $\mu^{\text{true}}/(1 + r)$, unchanged because average belief is unbiased.
(d) $(\mu^{\text{true}} + \Delta)/(1 + r)$, the optimist's unadjusted valuation.

>[!example]- Answer
>**(a)** Under the short-sale constraint, pessimists are corner-solution out of the market and optimists absorb the entire supply. Market-clearing with the optimist demand $x^1 = (\mu^1 - p(1 + r))/(\theta\sigma^2) = 1$ yields $p = (\mu^1 - \theta\sigma^2)/(1 + r)$; plugging in $\mu^1 = \mu^{\text{true}} + \Delta$ and market supply normalized to $1$ gives the answer. Note the $-2\theta\sigma^2$ arises because the optimist must be compensated for bearing *all* the risk alone (rather than half), so the risk premium doubles. The key point is that the price exceeds the frictionless fundamental.

## Question 5

**(Lecture $16$ — Household Finance.)** In Berk and Green ($2004$), active fund managers possess genuine skill, and investors are fully rational and Bayesian. Under these assumptions, what should the average *after-fee* alpha of active funds be in equilibrium?

(a) Strictly positive, because managers earn rents from their skill that they share with investors.
(b) Strictly negative, because fund expenses drag down any genuine alpha managers produce.
(c) Exactly zero, because flows respond to past performance until the marginal fund is indifferent to investing.
(d) Indeterminate — depends entirely on the aggressiveness of fee-setting by fund families.

>[!example]- Answer
>**(c) Exactly zero.** Berk-Green is the frictionless rational benchmark: skilled managers generate gross alpha, but flows chase past performance and drive fund size up until decreasing returns to scale eat exactly the skill-based alpha, leaving average after-fee alpha at zero. This is the benchmark that the *empirical* underperformance of active funds (Gruber $1996$, Fama-French $2010$) violates — active funds average *negative* after-fee alpha, not zero. The zero-alpha benchmark is what makes the puzzle a puzzle.

## Question 6

**(Lecture $13$ — Reaction Models.)** In Barberis, Shleifer, and Vishny ($1998$), an investor observes a long streak of earnings surprises in the same direction. According to the model, what does the investor infer?

(a) That the firm is still in Regime $1$ (conservatism), so she continues to underreact.
(b) That the firm has transitioned to Regime $2$ (representativeness), so she extrapolates the streak and overreacts.
(c) That the firm is in a new regime entirely outside the model's two-state structure.
(d) That the signal-to-noise ratio has fallen, so she weights the streak *less* than each individual surprise.

>[!example]- Answer
>**(b) Regime $2$.** BSV's investor starts with a strong prior on Regime $1$ (conservatism: earnings are a random walk, surprises are noise to ignore). A *long streak* is unlikely under Regime $1$ but likely under Regime $2$ (trend), so Bayesian updating inside the investor's (mis-specified) model shifts posterior weight to Regime $2$ and she begins extrapolating. The result is short-run underreaction (from early Regime-$1$ persistence) followed by long-run overreaction (from eventual Regime-$2$ extrapolation) — the unified explanation BSV advertise.

# Section 2 — Short Questions ($40$ points)

*Each question is worth $8$ points. Answers should be brief but complete.*

## Question 1

**(Lecture $14$ — Belief Biases.)** Write down the Rabin ($1998$) parametric family for distortions of Bayes' rule, identify the four corners $(c \lessgtr 1, d \lessgtr 1)$, and name the bias associated with each corner.

>[!example]- Answer
>$$\frac{\pi(A \mid S)}{\pi(B \mid S)} = \left(\frac{p(S \mid A)}{p(S \mid B)}\right)^c \left(\frac{\pi(A)}{\pi(B)}\right)^d$$
>
>Four corners:
>- $c < 1, d = 1$: **conservatism** — under-weighting new signals.
>- $c > 1, d = 1$: **overreaction** — over-weighting new signals, the cognitive root of long-run reversal.
>- $c = 1, d < 1$: **base-rate neglect** — under-weighting the prior, generating the representativeness heuristic.
>- $c = 1, d > 1$: **confirmation bias** — over-weighting the prior, generating belief polarization and asymmetric absorption of disconfirming evidence.
>
>The Bayesian benchmark is $c = d = 1$.

## Question 2

**(Lecture $18$ — Narrow Framing and Myopic Loss Aversion.)** Benartzi and Thaler ($1995$) propose *myopic loss aversion* as an explanation for the equity premium puzzle. Identify the two ingredients that must both be present, and briefly explain why *loss aversion alone* is insufficient.

>[!example]- Answer
>The two ingredients are **(i) loss aversion** and **(ii) narrow framing** — in particular, evaluating returns over short horizons (the lecture's working assumption is one-year evaluation windows).
>
>Loss aversion alone is insufficient because an agent who merges each new stock-market gamble with her *preexisting* wealth/portfolio will see that the gamble diversifies her other risks and *reduces* the total probability of a loss. Without narrow framing, the new gamble is evaluated jointly with existing holdings and loss aversion does not bite. Narrow framing forces the agent to evaluate the annual stock return *in isolation*, where the loss probability is around $30$–$40\%$; at that frequency, loss aversion makes equities unattractive and generates a required premium of the magnitude observed in the data.

## Question 3

**(Lecture $13$ — Long-Run Reversal.)** Describe De Bondt and Thaler ($1985$) — their construction of winner and loser portfolios, and the empirical finding — and explain why the result is a challenge to short-run momentum.

>[!example]- Answer
>De Bondt and Thaler rank all NYSE stocks by their prior $3$- to $5$-year returns, form a *loser* portfolio from the worst-performing decile and a *winner* portfolio from the best-performing decile, and track each portfolio's returns over the subsequent $3$–$5$ years. The loser portfolio outperforms the winner portfolio by roughly $25$ percentage points cumulative over three years.
>
>This is a **long-run reversal**: stocks that lost over the past $3$–$5$ years *win* over the next $3$–$5$ years, and vice versa. It sits in tension with Jegadeesh and Titman's *short-run momentum* ([[8.8. Momentum]]): at $3$–$12$-month horizons returns continue, but at $3$–$5$-year horizons they reverse. Any unified model of investor psychology must generate both — BSV and Hong-Stein ([[8.9. Reaction Models]]) are attempts to do so.

## Question 4

**(Lecture $17$ — Value Function Shape.)** State the three key features of Kahneman and Tversky's value function $v(\cdot)$, and for each, identify one empirical phenomenon it explains.

>[!example]- Answer
>**1. Reference dependence.** $v(\cdot)$ depends on gains and losses relative to a reference point, not on final wealth levels. Explains framing effects: the same final position is evaluated differently depending on whether it is framed as a gain or a loss (Kahneman-Tversky Example A: the "\$$1000$-then-choose" vs. "\$$2000$-then-choose" reversal).
>
>**2. Loss aversion.** $v(\cdot)$ has a kink at the origin with $\lim_{x \to 0^-} v'(x) > \lim_{x \to 0^+} v'(x)$, typically with loss slope about $2.25$ times gain slope. Explains small-stake risk aversion: rejection of a $50{:}50$ bet to win \$$110$ or lose \$$100$, which expected utility cannot generate for a reasonable concave utility.
>
>**3. Diminishing sensitivity.** $v(\cdot)$ is concave over gains but convex over losses. Explains risk-seeking in the loss domain: the preference for $(-\$1000, 1/2)$ over $(-\$500, 1)$, which is the empirical basis of the disposition effect (investors hold losers hoping for a bounce) and the "double down" phenomenon.

## Question 5

**(Lecture $16$ — Disposition Effect.)** Define the disposition effect using the PGR and PLR measures introduced by Odean ($1998$), and briefly explain how prospect theory ([[8.5.1. Prospect Theory]]) generates it.

>[!example]- Answer
>The proportion of realized gains and losses are
>$$\text{PGR} = \frac{\text{Realized Gains}}{\text{Realized Gains} + \text{Paper Gains}}, \qquad \text{PLR} = \frac{\text{Realized Losses}}{\text{Realized Losses} + \text{Paper Losses}}.$$
>The **disposition effect** is the empirical finding $\text{PGR} > \text{PLR}$ — investors realize gains at a higher rate than they realize losses of the same magnitude.
>
>Prospect theory generates this via *reference dependence* (the purchase price becomes the reference point) plus *diminishing sensitivity*. A winner sits in the concave gain region where the investor is risk-averse, so she prefers the sure gain of selling now to the uncertain additional gain of holding. A loser sits in the convex loss region where the investor is risk-seeking, so she prefers the gamble of holding (hoping for a rebound) to the sure loss of selling. The asymmetric curvature of the value function around the reference point is what pushes PGR above PLR.

# Section 3 — Barberis, Shleifer, and Vishny ($1998$): A Model of Investor Sentiment ($30$ points)

## Question 1

**(Lecture $13$ — BSV Structure.)** Describe the two-regime structure of the BSV ($1998$) model. In particular: what does each regime represent, which cognitive bias underlies each, and what is the investor's prior over the two regimes?

>[!example]- Answer
>BSV's investor believes that earnings follow one of two regimes, even though in reality they follow a random walk:
>- **Regime $1$: mean-reverting.** Positive earnings surprises are likely to be followed by negative ones; the investor treats each surprise as noise around a stable mean. This regime captures **conservatism bias** — the tendency to be slow in updating beliefs.
>- **Regime $2$: trending.** Positive surprises are likely to be followed by more positive ones; the investor treats the most recent surprises as informative about an underlying growth rate. This regime captures the **representativeness heuristic** — the tendency to see short streaks as representative of the generating process.
>
>The investor's prior places *more weight on Regime $1$* — she believes the world is *usually* mean-reverting. As she watches successive earnings announcements, she Bayesian-updates (within her mis-specified two-regime model) over which regime she is in.

## Question 2

**(Lecture $13$ — Reconciling Under- and Over-reaction.)** Explain how the BSV investor's updating produces short-run underreaction and long-run overreaction to a persistent stream of positive earnings news.

>[!example]- Answer
>After one or two positive surprises, the investor's prior on Regime $1$ (mean-reversion) dominates, so she treats the surprises as noise and barely updates her valuation. The stock's price rises *less* than the fundamental value warrants — this is **short-run underreaction**, matching the post-earnings-announcement drift of Bernard and Thomas ($1989, 1990$) and the short-run momentum of Jegadeesh and Titman ($1993$).
>
>As the streak continues, the posterior likelihood of Regime $2$ (trend) grows until the investor switches and begins extrapolating the streak. At this point she projects the trend forward and pushes the price *above* the true fundamental value — this is **long-run overreaction**, matching the long-run reversal of De Bondt and Thaler ($1985$). Eventually the trend breaks (because earnings are actually a random walk), the price corrects downward, and the reversal is realized.
>
>The key economic insight is that one investor, one set of information, and two cognitive biases can produce *both* empirical regularities by changing only the length of the observed history.

## Question 3

**(Lecture $13$ — Joint Empirical Prediction.)** State one empirical prediction that distinguishes BSV from a pure-rational benchmark, and describe how you would test it with cross-sectional stock data. Be specific about the sort and the expected sign of the effect.

>[!example]- Answer
>**Prediction.** BSV implies a specific *joint* time-series pattern: in the cross-section of stocks, those with the longest recent streaks of same-signed earnings surprises should exhibit *both* the strongest short-run momentum *and* the strongest subsequent long-run reversal. A pure-rational benchmark has no reason to predict post-announcement drift at all, let alone drift conditional on streak length.
>
>**Test design.** For each month $t$, sort all listed stocks into quintiles by the length of their streak of positive earnings surprises ending at $t$. For each quintile, compute:
>1. *Short-run cumulative abnormal return* over months $t+1$ through $t+12$ (the momentum window).
>2. *Long-run cumulative abnormal return* over months $t+13$ through $t+60$ (the reversal window).
>
>**Expected result under BSV.** The top streak-length quintile should show the strongest short-run momentum *and* the strongest subsequent long-run reversal — a positive correlation between momentum magnitude and reversal magnitude across quintiles. Under rational pricing, both patterns should be zero; under a mechanical momentum story without the Regime-$2$ switch, long-run reversal should be absent. Observing the *joint* pattern, cross-sectionally aligned, is the diagnostic signature of BSV.

# Section 4 — Prospect Theory Calculation ($20$ points)

**(Lecture $17$–$18$ — Loss Aversion and Narrow Framing.)**

Consider an investor with a prospect-theory value function
$$v(x) = \begin{cases} x & \text{if } x \geq 0, \\ \lambda x & \text{if } x < 0, \end{cases}$$
where $\lambda = 2.25$ is the loss aversion coefficient. The reference point is current wealth (so all gains and losses are measured from zero). Assume no probability weighting ($w(p) = p$).

## Part 1 ($8$ points)

The investor is offered a one-shot $50{:}50$ gamble to **win \$$200$** or **lose \$$100$**. Compute the prospect value of the gamble and state whether the investor accepts it.

>[!example]- Answer
>The prospect value is
>$$V = 0.5 \cdot v(200) + 0.5 \cdot v(-100) = 0.5 \cdot 200 + 0.5 \cdot (-2.25 \cdot 100) = 100 - 112.5 = -12.5.$$
>Since $V < 0$, the investor **rejects** the gamble, even though its expected monetary value is $+\$50$. Loss aversion alone ($\lambda > 1$) is enough to flip a strictly favorable small-stake bet into a rejection — this is the microfoundation of the equity premium puzzle via myopic loss aversion.

## Part 2 ($6$ points)

Now the investor is offered **two independent copies** of the same gamble, bundled together (so she evaluates them as a single compound prospect). The joint distribution is: win \$$400$ with probability $0.25$, net zero (win $200$ and lose $100$) with probability $0.5$, lose \$$200$ with probability $0.25$. Compute the prospect value and state whether she accepts.

>[!example]- Answer
>$$V = 0.25 \cdot v(400) + 0.5 \cdot v(100) + 0.25 \cdot v(-200)$$
>$$= 0.25 \cdot 400 + 0.5 \cdot 100 + 0.25 \cdot (-2.25 \cdot 200) = 100 + 50 - 112.5 = 37.5.$$
>Now $V > 0$, and she **accepts**. The bundled gamble is favorable because the middle outcome ($+100$) turns a would-be loss into a small gain, which pulls the average prospect value into positive territory. Merging independent gambles reduces the effective probability of a loss and lets loss aversion relax.

## Part 3 ($6$ points)

Explain why the comparison between Parts $1$ and $2$ is the central mechanism in Benartzi and Thaler's ($1995$) myopic-loss-aversion explanation of the equity premium puzzle. What role does the *frequency of portfolio evaluation* play?

>[!example]- Answer
>Parts $1$ and $2$ show that the same underlying risky asset can be either rejected or accepted depending on how finely the agent slices it into evaluation windows. If the stock market is evaluated *annually* (Part $1$-style, one draw at a time), loss aversion bites on each year's $\sim 30\%$ probability of a negative return and the agent demands a large premium to hold equities. If the stock market is evaluated over a *multi-decade horizon* (Part $2$-style, many independent draws bundled), the probability of a net loss approaches zero and loss aversion disengages; the agent would hold equities at a much lower required premium.
>
>Benartzi and Thaler compute that the **empirically observed equity premium** is consistent with myopic loss aversion at an evaluation horizon of roughly **one year**. Investors behave *as if* they re-evaluate their portfolios annually — not because a rational Bayesian would do so, but because of narrow framing. The narrower the framing window, the larger the required equity premium. Merging the short-horizon gambles mechanically (as the investor's natural compounding does) would eliminate the puzzle; only the psychological choice to keep framing narrowly preserves it.

# Topic Coverage Map

The table below shows which lecture each question draws from and which vault note it pairs with, for targeted review.

| Question | Lecture(s) | Topic Class | Relevant Vault Note |
|---|---|---|---|
| MC $1$ | $17$–$18$ | Prospect Theory | [[8.5.1. Prospect Theory]] |
| MC $2$ | $12$ | Preferences | [[8.10.6. Hyperbolic Discounting]] |
| MC $3$ | $14$ | Belief Biases | [[8.6.1. Conservatism]], [[8.6.2. Overreaction]] |
| MC $4$ | $15$ | Bubbles / Limits to Arbitrage | [[8.7. Bubbles]] |
| MC $5$ | $16$ | Household Finance | [[8.10.7. Active Fund Underperformance]] |
| MC $6$ | $13$ | Reaction Models | [[8.9.1. Barberis-Shleifer-Vishny Model]] |
| SQ $1$ | $14$ | Belief Biases | [[Economics/1. Finance/8. Behavioral Finance/8.6. Belief-Based Biases/8.6. Belief-Based Biases\|8.6. Belief-Based Biases]] |
| SQ $2$ | $18$ | Prospect Theory | [[8.5.1. Prospect Theory]] |
| SQ $3$ | $13$ | Reaction / Reversal | [[8.8. Momentum]] |
| SQ $4$ | $17$ | Prospect Theory | [[8.5.1. Prospect Theory]] |
| SQ $5$ | $16$ | Household Finance | [[8.10.3. Disposition Effect]] |
| Long Q (BSV) | $13$ | Reaction Models | [[8.9. Reaction Models]] |
| Problem (PT) | $17$–$18$ | Prospect Theory | [[8.5.1. Prospect Theory]] |

# See Also

- [[8. Behavioral Finance]] — top-level course hub.
- [[8.5. Prospect Theory]] — folder containing the prospect theory family.
- [[Economics/1. Finance/8. Behavioral Finance/8.6. Belief-Based Biases/8.6. Belief-Based Biases|8.6. Belief-Based Biases]] — folder containing the Rabin parametric family.
- [[8.9. Reaction Models]] — BSV and Hong-Stein hubs.
- [[8.10. Behavioral Household Finance]] — Berk-Green, disposition effect, hyperbolic discounting.
