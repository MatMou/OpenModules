# Block 3.2 — Habit Formation: State-Dependent Risk Aversion and the Dynamics of Fear

> *"The key insight of habit formation is that investors become more risk averse when the economy deteriorates — not because their preferences change, but because the same preference structure interacts differently with a changed economic state."*
> — John Campbell and John Cochrane, *Journal of Political Economy* (1999)

---

## Where We Left Off

Block 3.1 established the equity premium puzzle with precision: the standard CRRA representative-agent model, calibrated to observed consumption growth dynamics, implies equity premia orders of magnitude smaller than those observed in the data. The HJ bound made the problem model-free: any valid SDF must be far more volatile than the CRRA SDF, given the smoothness of aggregate consumption. The fundamental challenge is therefore to build models in which the pricing kernel is highly volatile — in which marginal utility swings dramatically with economic conditions — without either assuming implausibly high risk aversion or contradicting the observed smoothness of consumption growth.

Habit formation is the first and most canonical proposed resolution. Its central insight is elegant: what matters for marginal utility is not the *level* of consumption, but consumption *relative to some reference point* — a habit, a subsistence level, or the consumption of one's peers. When this reference point is itself time-varying and persistent, marginal utility becomes highly sensitive to even small movements in consumption, generating the SDF volatility required by the HJ bound. The mechanism does not require high curvature of the utility function per se; it requires that the agent be operating close to the habit threshold, where even small changes in consumption have large effects on welfare.

This block develops the habit formation framework in full, from its motivations and alternative specifications to the complete Campbell-Cochrane model and its empirical implications. We will see that habit formation does not merely fix the equity premium — it generates a rich set of predictions about return predictability, the cyclicality of risk premia, and the time-series behavior of the price-dividend ratio that make it one of the most empirically productive frameworks in modern asset pricing.

---

## 1. The Motivation for Habit Formation

### Psychological and Empirical Foundations

The idea that utility depends on relative rather than absolute consumption has deep roots in economics and psychology. Duesenberry (1949) argued that consumer satisfaction depends on one's consumption relative to others — the "keeping up with the Joneses" effect — and that the ratio of consumption to a social reference point is what enters the utility function, not the level alone. This insight was largely set aside by the Friedman-Modigliani permanent income framework, which focused on consumption levels, but it resurfaced in the asset pricing literature precisely because the level-based approach could not explain financial data.

Kahneman and Tversky's (1979) prospect theory provided a psychological foundation: people evaluate outcomes relative to a reference point, and losses relative to that reference are more painful than equivalent gains are pleasurable. While prospect theory involves loss aversion and probability weighting — features distinct from the habit formation framework — it shares the central insight that reference points matter enormously for well-being.

In the macroeconomic literature, the habit hypothesis helps explain two anomalies of the permanent income model. First, consumption growth exhibits **excess smoothness** — it responds less to permanent income shocks than the standard model predicts. Second, consumption responds to **predictable income changes** — the well-documented excess sensitivity puzzle. Habit formation models can generate both phenomena because agents with habits are more reluctant to adjust consumption in response to income news, having internalized the welfare cost of subsequently having to reduce consumption below a risen habit level.

### The Two Varieties: External and Internal Habits

Before developing the mathematics, it is important to distinguish two fundamentally different specifications of habit formation, which differ in whether the agent internalizes the effect of current consumption on future habit.

**External (Catching Up with the Joneses) Habits**: The habit stock $h_t$ depends on *aggregate* consumption, not the individual agent's own past consumption. Abel (1990) formalized this as:

$$
u(c_t, h_t) = \frac{(c_t/h_t)^{1-\gamma}}{1-\gamma}, \quad h_t = C_{t-1}^\alpha
$$

where $C_{t-1}$ is lagged *aggregate* consumption. In this specification, the individual agent takes $h_t$ as given — it is determined by the aggregate economy, not by her own choices. She therefore does not internalize the cost of raising her future habit when she consumes more today. The Euler equation has the standard form, since the agent treats $h_t$ as exogenous.

**Internal (Catching Up with Oneself) Habits**: The habit stock depends on the agent's *own* past consumption. She internalizes that consuming more today raises her future habit and makes future consumption less enjoyable. The Euler equation then contains additional terms reflecting this internalization — the agent effectively faces a higher implicit cost of current consumption.

The Campbell-Cochrane (1999) model — the dominant model in the literature — specifies an external habit over aggregate consumption. In equilibrium, with a representative agent, the agent's consumption equals aggregate consumption, so the distinction between internal and external matters for the Euler equation derivation but not for the equilibrium outcomes. External habits are analytically more tractable and are the standard in the asset pricing literature.

---

## 2. The Surplus Consumption Ratio: The Key State Variable

The conceptual heart of the habit formation approach is the **surplus consumption ratio**:

$$
S_t = \frac{c_t - h_t}{c_t}
$$

This is the fraction of current consumption that exceeds the habit level — the "breathing room" above subsistence. It is the central state variable in the Campbell-Cochrane model, and understanding its role is essential for everything that follows.

When $S_t$ is large, the agent is consuming well above her habit: she is comfortable, her marginal utility is relatively low, and she is not particularly averse to risk. When $S_t$ is small — when consumption has fallen close to the habit threshold — the agent is near her subsistence level. A further small decline in consumption would push her below habit, causing a dramatic increase in marginal utility. In this state, the agent is extremely averse to any risk that might reduce her consumption further.

### The Marginal Utility Calculation

With utility $u(c_t, h_t) = (c_t - h_t)^{1-\gamma}/(1-\gamma)$, marginal utility is:

$$
u'(c_t) = (c_t - h_t)^{-\gamma} = \left(S_t c_t\right)^{-\gamma} = S_t^{-\gamma} c_t^{-\gamma}
$$

The SDF is therefore:

$$
m_{t+1} = \beta \frac{u'(c_{t+1})}{u'(c_t)} = \beta \left(\frac{S_{t+1}}{S_t}\right)^{-\gamma} \left(\frac{c_{t+1}}{c_t}\right)^{-\gamma}
$$

Compare this to the standard CRRA SDF: $m^{CRRA}_{t+1} = \beta (c_{t+1}/c_t)^{-\gamma}$. The habit SDF has an additional multiplicative term $(S_{t+1}/S_t)^{-\gamma}$. When $S_{t+1}$ falls relative to $S_t$ — when the surplus consumption ratio declines, meaning consumption falls toward the habit — this term exceeds one and amplifies the SDF. If $S_t$ is small, the ratio $S_{t+1}/S_t$ can be very different from one even for modest changes in the level of consumption. This is the volatility amplification mechanism.

The local coefficient of relative risk aversion can be computed:

$$
RRA_t = -\frac{c_t \, u''(c_t, h_t)}{u'(c_t, h_t)} = \frac{\gamma}{S_t}
$$

When $S_t = 1$ (no habit, consumption far above the threshold), $RRA_t = \gamma$ — the standard result. But when $S_t = 0.05$ (consumption only 5% above habit), $RRA_t = 20\gamma$. With $\gamma = 2$ and $S_t = 0.05$, the effective risk aversion is $40$ — well within the range needed to explain the equity premium. Habit formation achieves high effective risk aversion during bad times without requiring high curvature of the underlying utility function.

---

## 3. The Campbell-Cochrane Model

### Consumption Process

Campbell and Cochrane (1999) assume that log consumption growth follows an i.i.d. process:

$$
\Delta \ln c_{t+1} = g + v_{t+1}, \quad v_{t+1} \sim \mathcal{N}(0, \sigma^2)
$$

where $g$ is the mean growth rate and $\sigma$ is the standard deviation. This is deliberately simple — the richness of the model comes from the habit dynamics, not from the consumption process.

### Habit Process and the Sensitivity Function

The key modeling choice is the specification of how the log surplus consumption ratio $s_t = \ln S_t$ evolves. Campbell and Cochrane specify:

$$
s_{t+1} = (1-\phi){\bar{s}} + \phi s_t + \lambda(s_t) \cdot v_{t+1}
$$

where $\bar{s} = \ln \bar{S}$ is the steady-state log surplus consumption ratio, $\phi \in (0,1)$ governs the persistence of habit, and $\lambda(s_t)$ is the **sensitivity function** — the key free function in the model. It controls how strongly the surplus ratio responds to consumption shocks.

The sensitivity function is chosen by Campbell and Cochrane to satisfy three properties that jointly pin it down almost uniquely:

**Property 1: The risk-free rate is constant.** This is a simplifying assumption that rules out risk-free rate variation as a source of return predictability, allowing the model to focus on equity premium dynamics. It imposes a constraint on $\lambda(s_t)$ that must hold for all values of $s_t$.

**Property 2: The habit is predetermined at the steady state.** In the steady state, the habit should not respond to consumption shocks — the sensitivity function should equal zero when $s_t$ is at its maximum $s_{max}$, beyond which the habit is at its lower bound of sensitivity.

**Property 3: The habit is non-negative.** Consumption must always exceed the habit: $c_t > h_t$, equivalently $S_t > 0$ and $s_t > -\infty$. The sensitivity function must prevent $s_t$ from falling below the lower bound.

These three properties yield the solution:

$$
\lambda(s_t) = \frac{1}{\bar{S}} \sqrt{1 - 2(s_t - \bar{s})} - 1
$$

valid for $s_t \leq s_{max} = \bar{s} + \frac{1}{2}(1 - \bar{S}^2)$, and $\lambda(s_t) = 0$ for $s_t > s_{max}$.

The resulting log SDF is:

$$
\ln m_{t+1} = \ln\beta - \gamma g - \gamma(1 + \lambda(s_t)) v_{t+1} - \gamma(\phi - 1)(s_t - \bar{s})
$$

The term $\gamma(1 + \lambda(s_t))$ is the **effective risk aversion** coefficient — how strongly the SDF responds to consumption shocks. At the steady state $s_t = \bar{s}$:

$$
\gamma(1 + \lambda(\bar{s})) = \gamma\left(1 + \frac{1}{\bar{S}} - 1\right) = \frac{\gamma}{\bar{S}}
$$

which matches the local risk aversion formula derived earlier. When $s_t$ is low (bad times), $\lambda(s_t)$ is large, effective risk aversion is high, and the SDF is very volatile. This is the state-dependent risk aversion that drives the model.

### Calibration

Campbell and Cochrane calibrate their model to match four moments of US data over the period 1890–1994:

| Moment | Data | Model |
|:---|---:|---:|
| Mean equity premium | 3.84% | 3.84% |
| Standard deviation of returns | 18.7% | 18.4% |
| Mean risk-free rate | 0.94% | 0.94% |
| Standard deviation of risk-free rate | 5.44% | 0% |

With $\gamma = 2$, $g = 1.89\%$, $\sigma = 1.50\%$, and $\phi = 0.87$, the model matches the first three moments by construction (they are used to identify the parameters). The zero volatility of the risk-free rate reflects the constant-$r_f$ assumption. The key parameter is $\bar{S} = 0.057$ — the steady-state surplus consumption ratio of just 5.7%, implying a steady-state effective risk aversion of $\gamma/\bar{S} = 2/0.057 \approx 35$.

---

## 4. Asset Pricing Implications

### The Equity Premium and Time-Varying Risk Premia

The conditional equity premium in the model is:

$$
\mathbb{E}_t[R^{eq}_{t+1}] - R_f \approx \gamma(1 + \lambda(s_t)) \cdot \sigma \cdot \sigma_{eq}
$$

This is *time-varying*. In bad times when $s_t$ is low, $\lambda(s_t)$ is large, risk aversion is high, and the equity premium is high. In good times when $s_t$ is near its maximum, $\lambda(s_t) \approx 0$, risk aversion equals the fundamental $\gamma$, and the equity premium is low.

This countercyclical variation in the equity premium is one of the model's most striking predictions — and one of its strongest empirical successes. There is substantial evidence that equity risk premia vary over the business cycle: premia are high in recessions and low in expansions. The price-earnings ratio, the dividend yield, the term spread, and the credit spread all predict equity returns in the time series, consistent with time-varying risk premia. Campbell and Cochrane (1999) show that their model generates return predictability of broadly the right magnitude and sign.

### The Price-Dividend Ratio

In the model, the price-dividend ratio $P_t/D_t$ is a function of the state variable $s_t$ alone (since consumption equals dividends in the endowment economy). When $s_t$ is low — bad times — the equity premium is high and the discount rate for future dividends is high, driving down the price-dividend ratio. When $s_t$ is high — good times — the equity premium is low and the price-dividend ratio is high.

This comovement generates **excess volatility**: stock prices are more volatile than the present value of future dividends discounted at a constant rate, because the discount rate itself varies. Shiller (1981) first documented this excess volatility puzzle — that stock price volatility exceeds the bound implied by constant-discount-rate valuation — and habit formation is one of the canonical resolutions. The time-varying equity premium generates time-varying discount rates that make prices volatile even when fundamental cash flows (dividends/consumption) are smooth.

### Return Predictability

The time-variation in $s_t$ generates predictability of equity returns. Since $s_t$ is persistent ($\phi = 0.87$), periods of low $s_t$ are followed by continued low $s_t$ — bad states tend to persist. During these bad states, expected returns are high. This means that variables correlated with $s_t$ — such as the price-dividend ratio or the consumption-wealth ratio — should predict future returns.

More precisely, the model predicts that:
- The **dividend yield** ($D/P$) should positively predict future excess returns: low prices relative to dividends signal high future risk premia.
- The **consumption-wealth ratio** (cay), proposed by Lettau and Ludvigson (2001) as a proxy for the surplus consumption ratio, should positively predict excess returns.
- Return predictability should be stronger at **longer horizons**, since the predictable component of returns (driven by the persistent state variable $s_t$) accumulates over time while the unpredictable component diversifies.

All three predictions have empirical support, though the strength and robustness of return predictability remains debated. The model therefore provides a coherent structural interpretation of the extensive empirical literature on return predictability — phenomena that would be puzzling under constant expected returns become natural consequences of time-varying risk aversion.

### The Sharpe Ratio

The conditional Sharpe ratio of equity in the Campbell-Cochrane model is:

$$
SR_t = \frac{\mathbb{E}_t[R^{eq}_{t+1}] - R_f}{\sigma_t(R^{eq}_{t+1})} = \gamma(1 + \lambda(s_t)) \cdot \sigma
$$

At the steady state: $SR = \gamma/\bar{S} \cdot \sigma = (2/0.057) \cdot 0.015 \approx 0.53$. This exactly matches the historical average Sharpe ratio of US equity — by construction, given the calibration. But the model goes further: the Sharpe ratio is **countercyclical**, rising in recessions. This is consistent with evidence from options markets, where implied volatility (and hence implied Sharpe ratios) spikes during market downturns.

---

## 5. The Model's Limitations

Despite its empirical successes, the Campbell-Cochrane model has important limitations that have motivated subsequent work.

### The Risk-Free Rate

The constant risk-free rate assumption, while analytically convenient, is counterfactual. Real interest rates vary substantially over time — they were high in the early 1980s, fell through the 1990s and 2000s, and have remained near zero (or below) since the financial crisis. The Campbell-Cochrane model, by construction, has nothing to say about interest rate dynamics. Any application of the model to bond pricing or term structure questions requires extending it in ways that are not trivial.

### The Consumption-Habit Specification

The model requires that $\bar{S} = 0.057$ — that steady-state consumption is only 5.7% above the habit level. This is a knife-edge calibration. The slightest shock drives the economy close to the habit boundary, where effective risk aversion explodes. Some argue this is an implausible description of actual household behavior — real agents do not seem to live in perpetual fear of falling below subsistence. The model requires agents to behave *as if* they are always close to the edge, even when by any objective measure they are not.

### The Welfare Implications

The high effective risk aversion in the Campbell-Cochrane model implies enormous welfare costs of consumption volatility. Using the model's parameters, the welfare cost of eliminating all consumption uncertainty is enormous — far larger than Lucas's (1987) original calculation of less than 0.1% of consumption. This raises the question of whether the model is internally consistent: if agents dislike uncertainty so intensely, why don't they take much stronger precautionary actions to smooth consumption?

### Long-Run Risk and the EIS

Campbell and Cochrane (1999) effectively set the EIS equal to $1/\gamma = 0.5$ (since they use power utility with $\gamma = 2$ as the fundamental preference). This is inconsistent with the evidence from the long-run risk literature (Bansal and Yaron, 2004), which suggests that matching both the equity premium and the risk-free rate requires a high EIS — precisely the separation that recursive preferences provide. Habit formation and recursive preferences are often seen as competing rather than complementary approaches, though models combining both have been explored.

### No Long-Run Risk

The i.i.d. consumption growth assumption means the model has no long-run predictable component in consumption — no persistence in expected growth rates. This is inconsistent with the evidence (Bansal and Yaron, 2004; Hansen, Heaton, and Li, 2008) that expected consumption growth is slowly time-varying. The long-run risk model of Block 3.4 addresses this directly.

---

## 6. Variants and Extensions

### Abel's Catching Up with the Joneses

Abel (1990) proposed a simpler external habit specification where utility is $u(c_t, C_{t-1}) = (c_t/C_{t-1}^\alpha)^{1-\gamma}/(1-\gamma)$, with $C_{t-1}$ being lagged aggregate consumption. This is a ratio habit (multiplicative) rather than a difference habit (additive). The ratio habit preserves the scale-invariance of CRRA preferences and generates a model where the equity premium depends on the ratio $\gamma\alpha$ — risk aversion times the strength of habit. While analytically tractable, this specification does not generate time-varying risk premia since the habit-adjusted consumption ratio has constant conditional volatility.

### Constantinides' Internal Habit Model

Constantinides (1990) developed an internal habit model in which the agent's own past consumption determines habit. This generates strong precautionary savings behavior and can match both the equity premium and the risk-free rate. However, the internal habit creates a wedge between the Euler equation and the standard formulation — the agent must account for the shadow cost of raising future habit — making the model more complex to solve and calibrate.

### The External Habit with Incomplete Markets

Combining habit formation with incomplete markets (Storesletten, Telmer, and Yaron, 2007; Brav, Constantinides, and Geczy, 2002) potentially addresses both the equity premium and the cross-sectional evidence on consumption risk. If individual consumption is exposed to idiosyncratic shocks that are countercyclically volatile, and if agents have habit preferences, the effective risk aversion during recessions is amplified along two dimensions simultaneously: the habit mechanism raises aggregate marginal utility sensitivity, while the idiosyncratic risk mechanism raises the dispersion of individual consumption experiences.

---

## 7. Connecting Habit Formation to the SDF Framework

The habit formation model can be fully expressed in the SDF language of Block 2.1. The model implies:

$$
m_{t+1} = \beta \left(\frac{c_{t+1}}{c_t}\right)^{-\gamma} \left(\frac{S_{t+1}}{S_t}\right)^{-\gamma}
$$

The second term — the ratio of surplus consumption ratios — is the habit formation "amplification factor." In the Campbell-Cochrane model, this term is highly correlated with the business cycle: it is large and variable in recessions, small and stable in expansions. This is exactly what the HJ bound requires — a volatile SDF that is especially high in bad states, commanding large risk premia for assets that pay off poorly in those states.

The HJ volatility of the habit SDF is:

$$
\frac{\sigma(m)}{\mathbb{E}[m]} \approx \gamma \sqrt{\text{Var}(\Delta \ln c_{t+1}) + \text{Var}(\Delta \ln S_{t+1}) + 2\text{Cov}(\Delta \ln c_{t+1}, \Delta \ln S_{t+1})}
$$

The surplus ratio term $\Delta \ln S_{t+1}$ adds substantially to the SDF volatility. Given the sensitivity function $\lambda(s_t) \approx 1/\bar{S} - 1 \approx 16.5$ at the steady state, the effective contribution of consumption shocks to SDF volatility is amplified by a factor of $1 + \lambda \approx 17.5$. The HJ bound of $0.5$ is met with $\gamma = 2$ rather than $\gamma = 50$ — a dramatic improvement.

This is the fundamental message of habit formation: **the volatility of the SDF does not require a volatile consumption path; it requires that small consumption fluctuations have large welfare consequences.** By operating near the habit threshold, the agent satisfies the HJ bound at moderate levels of fundamental risk aversion, resolving the equity premium puzzle without the need for implausible preference parameters — at the cost of requiring the economy to perpetually hover near the subsistence threshold.

---

## Key Takeaways

**Habit formation generates state-dependent risk aversion.** When consumption is close to the habit level — in recessions, in bad times — marginal utility is highly sensitive to further consumption declines. The local coefficient of relative risk aversion is $\gamma/S_t$, which can be very large when $S_t$ is small.

**The surplus consumption ratio $S_t = (c_t - h_t)/c_t$ is the key state variable.** It determines the level of effective risk aversion and therefore the conditional equity premium. Its dynamics drive all time-variation in risk premia.

**The Campbell-Cochrane model matches the unconditional equity premium and risk-free rate with $\gamma = 2**.** The amplification comes from the sensitivity function $\lambda(s_t)$, which ensures the constant risk-free rate condition while allowing the SDF to be highly volatile.

**The model generates countercyclical risk premia, excess volatility, and return predictability.** These are additional empirical successes beyond the unconditional moments. The time-varying equity premium rationalizes predictive regressions using the dividend yield and the consumption-wealth ratio.

**The model has important limitations.** The constant risk-free rate is counterfactual; the knife-edge calibration near the habit boundary is questionable; the EIS is pinned at $1/\gamma$, preventing the separation of risk aversion and intertemporal substitution; and the i.i.d. consumption process abstracts from long-run predictability.

**In SDF language, habit formation amplifies the volatility of the pricing kernel** far beyond what CRRA utility generates at the same parameters, satisfying the Hansen-Jagannathan bound at plausible risk aversion through the proximity of consumption to the habit threshold rather than through high fundamental curvature of preferences.

---

## Looking Ahead: Block 3.3 — Recursive Preferences and Long-Run Risk

The limitations of the Campbell-Cochrane model — particularly the conflation of risk aversion and EIS, and the lack of long-run predictability in consumption — motivate an alternative approach. Block 3.3 introduces **Epstein-Zin recursive preferences**, which break the CRRA constraint that $EIS = 1/\gamma$. With high risk aversion and high EIS simultaneously, the model can generate a low and stable risk-free rate alongside a large equity premium. Block 3.4 then combines recursive preferences with **long-run risk** in consumption — the key innovation of Bansal and Yaron (2004) — to show that the fear of small, persistent changes in long-run growth prospects can generate large risk premia without any of the habit machinery. Together, these two blocks represent the dominant alternative paradigm to habit formation in modern consumption-based asset pricing.

---

*Block 3.1 — The Equity Premium Puzzle | **Block 3.2 — Habit Formation** | Block 3.3 — Recursive Preferences →*
