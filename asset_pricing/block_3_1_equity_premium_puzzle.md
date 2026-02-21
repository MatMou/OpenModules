# Block 3.1 — The Equity Premium Puzzle and Its Discontents

> *"The equity premium is a major embarrassment for the paradigm of economic theory based on market clearing, rational expectations, and expected utility maximization. The data clearly suggest that people are far more averse to risk than the theory predicts."*
> — Rajnish Mehra, *Handbook of the Economics of Finance* (2003)

---

## Where We Left Off

Part 2 built the complete structural language of asset pricing — the SDF, the mean-variance frontier, the CAPM, the APT, and the factor zoo. These are the tools with which we describe and test pricing models. But description is not explanation. The central quantitative challenge for any asset pricing model grounded in economic fundamentals is to *account* for observed risk premia from first principles: to show that the observed return difference between equities and Treasury bills — roughly 6–7% per annum in US data over the twentieth century — is the natural compensation for the systematic risk that equity investors bear.

The equity premium puzzle is the finding that this task is essentially impossible within the standard consumption-based framework at any plausible level of risk aversion. First stated with precision by Mehra and Prescott (1985), the puzzle has shaped the entire agenda of modern asset pricing. Every serious model developed since — habit formation, recursive preferences, rare disasters, long-run risk — is in some sense a proposed resolution. Understanding the puzzle deeply, in its original form and in all the dimensions it subsequently acquired, is therefore a prerequisite for understanding the frontier of the field.

This block examines the puzzle in full: its derivation, the joint puzzle with the risk-free rate, the calibration methodology and its assumptions, the formal bounds that make the puzzle model-independent, and the landscape of proposed resolutions. It is the bridge from the structural framework of Part 2 to the richer models of Parts 3 and 4.

---

## 1. The Puzzle: Original Setup and Derivation

### The Mehra-Prescott Economy

Mehra and Prescott (1985) worked in the simplest possible equilibrium framework: a **Lucas (1978) endowment economy**. There is a single representative agent with CRRA utility:

$$
U = \mathbb{E}_0\left[\sum_{t=0}^{\infty} \beta^t \frac{c_t^{1-\gamma}}{1-\gamma}\right], \quad \gamma > 0, \; \beta \in (0,1)
$$

There is a single risky asset — a claim to aggregate consumption (the "Lucas tree") — and a one-period risk-free bond. There is no production; the endowment follows an exogenous process. In equilibrium, the agent must hold all the equity (market clearing requires the equity holding to equal one and bond holding to equal zero, since there is nothing to borrow from).

The fundamental pricing equation for any asset with gross return $R_{t+1}$ is the Euler equation:

$$
1 = \mathbb{E}_t\left[\beta \left(\frac{c_{t+1}}{c_t}\right)^{-\gamma} R_{t+1}\right]
$$

The SDF is $m_{t+1} = \beta (c_{t+1}/c_t)^{-\gamma}$. Mehra and Prescott modeled the consumption growth process as a two-state Markov chain, where in each period consumption grows by either $\lambda_1$ or $\lambda_2$ (with $\lambda_1 > \lambda_2$), and transitions between states follow a given probability matrix. This is deliberately parsimonious — the model has very few degrees of freedom, making calibration clean and transparent.

### The Calibration

Mehra and Prescott calibrated the model to match three moments of US macroeconomic data over the period 1889–1978:

- **Mean consumption growth**: $\mathbb{E}[\Delta \ln c] \approx 1.8\%$ per annum
- **Standard deviation of consumption growth**: $\sigma_c \approx 3.6\%$ per annum
- **First-order autocorrelation of consumption growth**: approximately $-0.14$

These three moments tightly constrain the parameters of the two-state Markov chain. The question then is: for what values of $(\gamma, \beta)$ does the model simultaneously match:

- **The equity premium**: $\mathbb{E}[R^{eq}] - R_f \approx 6.18\%$ per annum
- **The risk-free rate**: $R_f \approx 0.80\%$ per annum (approximately the real return on short-term Treasury bills)

### The Answer: An Order-of-Magnitude Failure

For a log-normal approximation, the equity premium in this model satisfies:

$$
\mathbb{E}[R^{eq}] - R_f \approx \gamma \cdot \text{Cov}\left(\Delta \ln c_{t+1}, r^{eq}_{t+1}\right) \approx \gamma \cdot \sigma_c \cdot \sigma_{eq} \cdot \rho_{c,eq}
$$

Since equity is a claim to consumption, $\rho_{c,eq} \approx 1$ in the model. With $\sigma_c \approx 3.6\%$ and $\sigma_{eq} \approx 15\%$ (the historical standard deviation of equity returns), and $\rho_{c,eq} \approx 1$:

$$
\mathbb{E}[R^{eq}] - R_f \approx \gamma \cdot 0.036 \cdot 0.15 \approx \gamma \cdot 0.0054
$$

To match the observed premium of $6.18\%$:

$$
\gamma \approx \frac{0.0618}{0.0054} \approx 11.4
$$

This does not yet sound catastrophic — $\gamma \approx 11$ is high but not absurd. But Mehra and Prescott showed through careful numerical analysis of their Markov chain model that the required $\gamma$ is actually much higher — in the range of $30$–$50$ — when the model is forced to simultaneously match the consumption growth process precisely. The reason is that in the calibrated model, the correlation between consumption growth and equity returns is imperfect, and the relevant covariance is smaller than the back-of-the-envelope suggests.

More importantly, they showed that the parameter space $\{(\gamma, \beta): \gamma \leq 10, \beta \leq 1\}$ — which they argued represented the economically plausible region — could generate a maximum equity premium of only about **0.35%** per annum. The observed **6.18%** is nearly **18 times larger**. This is not a quantitative failure but a qualitative one.

---

## 2. The Risk-Free Rate Puzzle

The equity premium puzzle is only half the story. Weil (1989) identified a companion puzzle — the **risk-free rate puzzle** — that makes the situation considerably worse.

### The Real Interest Rate in the Model

Under log-normality of consumption growth, the real risk-free rate in the Mehra-Prescott model satisfies:

$$
r_f = \delta + \gamma \mathbb{E}[\Delta \ln c] - \frac{\gamma^2}{2} \sigma_c^2
$$

where $\delta = -\ln\beta$ is the rate of time preference. This is the continuous-time Ramsey rule from Block 1.3, augmented by a precautionary savings term.

Now consider what happens when we try to match the equity premium by raising $\gamma$. Increasing $\gamma$ increases the second term ($\gamma \mathbb{E}[\Delta \ln c]$) and also increases the precautionary savings term. For reasonable mean consumption growth of $1.8\%$:

| $\gamma$ | $\gamma \mathbb{E}[\Delta \ln c]$ | Risk-free rate (approx.) |
|---:|---:|---:|
| 2 | 3.6% | ~5% |
| 10 | 18% | ~19% |
| 30 | 54% | ~55% |
| 50 | 90% | ~90% |

The model predicts an astronomically high risk-free rate when $\gamma$ is large. The observed real risk-free rate is approximately 0.8% per annum. To reconcile a high $\gamma$ with a low $r_f$, one would need an implausibly high discount factor $\beta > 1$ (agents are *more* patient about the future than the present) — a condition that would make the agent's lifetime utility diverge and violate the transversality condition.

The two puzzles are therefore **jointly** devastating:

- **Too low $\gamma$** implies an equity premium far below what we observe.
- **High $\gamma$** that would match the premium implies a risk-free rate far above what we observe.

There is no value of $(\gamma, \beta)$ in the standard model that simultaneously fits both. The data jointly require high risk aversion (to explain the premium) and low risk aversion or strong impatience (to explain the low risk-free rate). The standard CRRA framework cannot reconcile these.

---

## 3. The Hansen-Jagannathan Bounds: Making the Puzzle Model-Free

The Mehra-Prescott analysis was conducted within a specific model. One might object that their conclusion depends on particular functional form assumptions or on the Markov chain structure. The Hansen-Jagannathan bounds, derived in Block 2.1, show that the puzzle is entirely model-free.

Recall the HJ bound:

$$
\frac{\sigma(m)}{\mathbb{E}[m]} \geq \max_i \left|\frac{\mathbb{E}[R^i] - R_f}{\sigma(R^i)}\right|
$$

The right-hand side is the maximum Sharpe ratio achievable from any portfolio of traded assets. For US data, this is approximately $0.5$ per annum. The bound then requires that any valid SDF must have a coefficient of variation of at least $0.5$.

Under CRRA preferences, $m_{t+1} = \beta(c_{t+1}/c_t)^{-\gamma}$. A log-normal approximation gives:

$$
\frac{\sigma(m)}{\mathbb{E}[m]} \approx \sqrt{e^{\gamma^2 \sigma_c^2} - 1} \approx \gamma \sigma_c \quad \text{for small } \gamma \sigma_c
$$

With $\sigma_c \approx 1\%$ (annual per-capita consumption growth volatility in the postwar US), the HJ bound requires:

$$
\gamma \cdot 0.01 \geq 0.5 \quad \Longrightarrow \quad \gamma \geq 50
$$

Note the discrepancy with the earlier calculation. Mehra and Prescott used $\sigma_c \approx 3.6\%$ because they included the Great Depression era in their sample. Postwar data exhibits much smoother consumption growth — $\sigma_c$ drops to about $1\%$ — making the puzzle even more severe. Over the full historical sample, the constraint is $\gamma \geq 14$; over the postwar sample alone, it is $\gamma \geq 50$.

This is the power of the HJ framework: the puzzle holds regardless of the assumed utility function, preference specification, or equilibrium structure. It follows purely from the observed volatility of consumption growth, the observed Sharpe ratio of equity, and the requirement that prices be consistent with no-arbitrage. Any model that proposes to resolve the puzzle must either increase $\sigma(m)$ (by making the SDF more volatile) or decrease the maximum Sharpe ratio — and the latter is not available since we are trying to match observed asset prices.

---

## 4. Why Consumption Growth Is So Smooth: The Measurement Issue

Before concluding that the standard model is definitively wrong, one should ask whether the puzzle might reflect mismeasurement of the model's key input: aggregate consumption.

### Consumption Measurement Problems

The NIPA (National Income and Product Accounts) measure of per-capita consumption used in most empirical tests has several limitations:

**Time aggregation**: NIPA consumption data is measured at quarterly or annual frequency, time-averaging the underlying instantaneous consumption flows. Time averaging induces negative autocorrelation and reduces the variance of measured growth rates relative to true instantaneous growth. Grossman and Shiller (1981) showed that this alone can substantially reduce the measured volatility of consumption growth.

**Durables**: NIPA consumption includes expenditures on durable goods (cars, appliances), but the relevant measure for utility is the **service flow** from durables, not their purchase. Durable expenditure is far more volatile than service flows — and stock market returns are more highly correlated with durable expenditure than with non-durable consumption. Mankiw and Shapiro (1986) found that using non-durables and services consumption reduces the puzzle somewhat but does not resolve it.

**Aggregation**: NIPA consumption is aggregate per-capita consumption, averaging over a very large and heterogeneous population. If risk sharing is imperfect — if households cannot fully insure each other against idiosyncratic income shocks — then aggregate consumption may be much smoother than individual consumption. A representative agent model calibrated to aggregate consumption will understate the true degree of risk that individual households face. This is the **limited market participation** and **incomplete markets** channel, which we develop in Block 3.3.

**Stockholder consumption**: Most households hold little or no equity. The relevant consumption for pricing equity is the consumption of the stockholding class — households who actually hold the equity risk. Vissing-Jørgensen (2002) and Malloy, Moskowitz, and Vissing-Jørgensen (2009) showed that stockholder consumption growth is substantially more volatile and more highly correlated with equity returns than aggregate consumption. Using stockholder consumption reduces the required risk aversion coefficient considerably — though not to the levels usually considered plausible.

These measurement considerations are important and partially address the puzzle, but the consensus view is that they cannot fully account for a factor-of-50 discrepancy.

---

## 5. The Landscape of Proposed Resolutions

The equity premium puzzle has generated an enormous literature of proposed resolutions. We sketch the main approaches here, each of which will be developed in detail in subsequent blocks.

### Resolution 1: Habit Formation

Campbell and Cochrane (1999) proposed that utility depends not on the level of consumption but on **consumption relative to a habit stock** — a slow-moving average of past consumption:

$$
u(c_t, h_t) = \frac{(c_t - h_t)^{1-\gamma}}{1-\gamma}
$$

The key insight is that the **surplus consumption ratio** $S_t = (c_t - h_t)/c_t$ varies over time. When the economy is in a recession, $c_t$ falls close to the habit level $h_t$, making $S_t$ small and marginal utility very high. The SDF $m_{t+1} = \beta(c_{t+1} - h_{t+1})^{-\gamma}/(c_t - h_t)^{-\gamma}$ therefore becomes extremely volatile in recessions, generating large risk premia even with moderate $\gamma$.

Habit formation amplifies the volatility of the SDF by making marginal utility highly sensitive to the state of the economy — even when consumption itself moves relatively smoothly. We develop this model fully in Block 3.2.

### Resolution 2: Recursive Preferences (Epstein-Zin)

Epstein and Zin (1989) proposed a generalization of expected utility in which **risk aversion and the elasticity of intertemporal substitution (EIS) are separate parameters**. Under CRRA, both are tied to $\gamma$: risk aversion is $\gamma$ and EIS is $1/\gamma$. This coupling is the source of the tension between the equity premium puzzle and the risk-free rate puzzle.

With recursive preferences, an agent can simultaneously have:
- High risk aversion (large $\gamma$), generating a large equity premium.
- High EIS (large $\psi$), generating a low and stable risk-free rate.

Bansal and Yaron (2004) showed that combining recursive preferences with a **long-run risk** process for consumption growth — small but persistent predictable components in expected growth and volatility — generates large risk premia with plausible parameters. The key is that, with high EIS and recursive preferences, the agent is highly sensitive to news about the long-run prospects of the economy, generating volatile asset prices even when current consumption barely moves. We develop recursive preferences in Block 3.3 and long-run risk in Block 3.4.

### Resolution 3: Rare Disasters

Rietz (1988) first proposed that the equity premium could be justified by the rare but catastrophic possibility of economic disasters — events like the Great Depression, hyperinflations, or wars — during which both consumption and equity values collapse simultaneously. If such disasters carry positive probability, even a small expected return during normal times may be consistent with rational risk aversion once the disaster states are priced in.

Barro (2006) revived and formalized this argument using international data on macroeconomic disasters. He showed that cross-country data exhibit a fat left tail of catastrophic consumption declines, and calibrated the disaster probability and severity to match this data. With plausible disaster parameters and moderate risk aversion ($\gamma \approx 3$–$5$), the model generates equity premia and risk-free rates close to their historical values. The SDF occasionally takes enormous values in disaster states, contributing substantially to $\mathbb{E}[mR]$ even if the probability weight on those states is small. We develop this in Block 3.5.

### Resolution 4: Incomplete Markets and Idiosyncratic Risk

Mankiw (1986) and subsequent work by Heaton and Lucas (1996) and Constantinides and Duffie (1996) argued that the equity premium can be rationalized once we abandon the representative agent framework and allow for **idiosyncratic income risk that cannot be fully insured**. In incomplete markets, individual consumption is more volatile than aggregate consumption, and the cross-sectional distribution of consumption growth widens precisely in bad times — when aggregate consumption falls. This counter-cyclical dispersion of idiosyncratic risk is an additional source of systematic risk for equities that is absent from the representative-agent model. We examine this channel in Block 3.3.

### Resolution 5: Behavioral and Market Microstructure Approaches

Behavioral approaches challenge the rational expectations and expected utility assumptions rather than the preference parameters. Benartzi and Thaler (1995) proposed **myopic loss aversion**: investors evaluate their portfolios over short horizons and are loss-averse in the sense of Kahneman and Tversky's (1979) prospect theory. Even if the long-run return to equities is attractive, short-horizon investors who are loss-averse may demand a large premium for the possibility of interim losses. Barberis, Huang, and Santos (2001) formalized this in a general equilibrium model.

Other behavioral approaches invoke overreaction and underreaction to news, investor sentiment, and limited attention. These approaches do not resolve the HJ bound within a standard framework — they modify the objective function rather than the SDF structure — but they provide psychologically grounded accounts of the data patterns.

---

## 6. Why the Puzzle Matters Beyond Asset Pricing

The equity premium puzzle might seem like a narrow technical concern — a quantitative discrepancy in a calibrated model. Its significance, however, extends far beyond asset pricing:

**Cost of capital**: If equity risk premia are genuinely 6–7% per annum, this has enormous implications for corporate investment decisions, capital budgeting, and the cost of equity capital. If the true premium is much lower — as some argue the forward-looking premium is — the implications are equally large in the opposite direction.

**Social discount rate**: The Ramsey rule $r = \delta + \gamma g$ is used to compute the social discount rate for cost-benefit analysis of long-lived public projects, including climate policy. The equity premium puzzle, and the associated risk-free rate puzzle, directly bear on what discount rate governments should use. A high $\gamma$ implies high discounting of future benefits; a low $\gamma$ implies the opposite.

**Retirement savings**: The appropriate allocation between equities and bonds in pension funds and individual retirement accounts depends critically on the expected equity premium and the degree to which it represents genuine compensation for risk.

**Macroeconomic policy**: Models used for monetary and fiscal policy analysis — DSGE models — typically calibrate preference parameters to match financial moments. A model that cannot explain the equity premium also provides potentially misleading policy guidance.

The puzzle is therefore not merely an intellectual curiosity. It sits at the intersection of finance, macroeconomics, and economic policy, and its resolution matters for how we think about investment, growth, and the design of public institutions.

---

## 7. Taking Stock: What Any Resolution Must Accomplish

Before moving to specific proposed resolutions, it is useful to state clearly what any resolution must achieve. A satisfactory resolution must:

1. **Satisfy the HJ bound** at plausible parameter values — the SDF must be sufficiently volatile.
2. **Match the equity premium** of approximately 6% and the risk-free rate of approximately 1% jointly — not one at the expense of the other.
3. **Be consistent with observed consumption dynamics** — it cannot simply assert that consumption is much more volatile or correlated with returns than the data show.
4. **Generate plausible behavior** for other moments: the volatility and predictability of stock returns, the behavior of the price-dividend ratio, the term structure of interest rates, and consumption and savings behavior.
5. **Rest on economically meaningful mechanisms** — the modification to the standard model should have a clear interpretation in terms of preferences, market structure, or information, not merely be a mathematical device for fitting moments.

These are demanding criteria, and no single model satisfies all of them perfectly. The literature has produced a set of partial resolutions that each address some of the criteria while falling short on others. The state of the field is one of productive tension: we understand the puzzle far better than in 1985, but no consensus model has emerged.

---

## Key Takeaways

**The equity premium puzzle is the finding that the observed return premium on equity cannot be explained by the observed volatility of consumption growth at any plausible level of risk aversion.** The standard CRRA consumption-based model requires $\gamma \geq 30$–$50$ to match historical data, far outside the economically meaningful range.

**The risk-free rate puzzle is the companion finding** that raising $\gamma$ to match the equity premium implies a counterfactually high risk-free rate — the two moments cannot be simultaneously matched within the standard model.

**The Hansen-Jagannathan bound makes the puzzle model-free.** Any valid SDF must have a coefficient of variation of at least 0.5; the CRRA SDF achieves this only at $\gamma \geq 50$ given postwar US consumption volatility of 1%. This holds regardless of the assumed equilibrium structure.

**Measurement issues partially mitigate the puzzle** — time aggregation, the use of aggregate versus stockholder consumption, and the treatment of durables all affect the calibration — but cannot fully account for the magnitude of the discrepancy.

**The major proposed resolutions — habit formation, recursive preferences, rare disasters, incomplete markets — each modify a specific ingredient of the standard model to generate a more volatile SDF at plausible parameters.** None is fully satisfactory on all dimensions, and the puzzle remains a central challenge for the field.

**The puzzle's significance extends beyond asset pricing** to the social discount rate, retirement savings policy, and macroeconomic model calibration. Getting the equity premium right matters for a wide range of economic decisions.

---

## Looking Ahead: Block 3.2 — Habit Formation

The first proposed resolution we examine in depth is habit formation. Block 3.2 develops the Campbell-Cochrane (1999) model in full — the surplus consumption ratio, the specification of the habit process, the non-linear SDF dynamics, and the model's implications for the equity premium, the risk-free rate, the cyclicality of risk premia, and the predictability of stock returns. Habit formation is the canonical model of state-dependent risk aversion, and it generates a rich set of empirical predictions that go well beyond simply matching the first two moments of returns.

---

*Block 2.3 — Factor Models and the APT | **Block 3.1 — The Equity Premium Puzzle** | Block 3.2 — Habit Formation →*
