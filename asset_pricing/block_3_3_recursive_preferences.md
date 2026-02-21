# Block 3.3 — Recursive Preferences: Disentangling Risk Aversion from Intertemporal Substitution

> *"The separation of risk aversion and intertemporal substitution is not merely a technical generalization. It resolves a fundamental tension at the heart of the equity premium puzzle and opens an entirely new set of economic questions about the pricing of long-horizon risk."*
> — Ravi Bansal and Amir Yaron, *Journal of Finance* (2004)

---

## Where We Left Off

Block 3.2 developed the habit formation model as a resolution to the equity premium puzzle. Its central mechanism — operating near the habit threshold to achieve high effective risk aversion with low fundamental curvature — works well on the unconditional equity premium and generates rich predictions about return predictability and excess volatility. But the model carries a structural constraint: because it rests on standard expected utility with power preferences, the elasticity of intertemporal substitution (EIS) is mechanically tied to the coefficient of relative risk aversion (RRA) through the relationship $EIS = 1/\gamma$. With $\gamma = 2$, the EIS is $0.5$. With the high $\gamma$ needed to satisfy the HJ bound directly, the EIS collapses toward zero — implying an agent so reluctant to substitute consumption across time that she barely responds to interest rate changes at all.

This coupling is not merely an inconvenience. The risk-free rate puzzle of Block 3.1 showed that matching the equity premium requires high risk aversion while matching the low and stable risk-free rate requires something closer to high EIS. Under expected utility, these demands are fundamentally contradictory. Any model that hopes to simultaneously match both moments must break the $EIS = 1/\gamma$ constraint.

Epstein and Zin (1989) showed that this constraint is not a logical necessity but an artifact of the expected utility framework — specifically, of the compound lottery axiom that forces the utility function to be linear in probabilities. By relaxing this axiom while maintaining dynamic consistency and a recursive structure, they constructed a class of preferences in which RRA and EIS are genuinely independent parameters. This block develops their framework in full, derives the associated stochastic discount factor, and explores the profound implications for asset pricing — culminating in the insight that, with recursive preferences and high EIS, the agent becomes deeply sensitive to news about the *long-run* prospects of the economy, creating a powerful new channel for generating large risk premia.

---

## 1. What Is Wrong with Expected Utility in Dynamic Settings?

### The Time-Additivity Straitjacket

Standard expected utility in a dynamic setting takes the form:

$$
U_t = \mathbb{E}_t\left[\sum_{\tau=0}^{\infty} \beta^\tau u(c_{t+\tau})\right]
$$

This formulation has two distinct components bundled together: (1) **risk aversion**, captured by the curvature of $u$, which governs how much the agent dislikes contemporaneous gambles; and (2) **intertemporal substitution**, governed by how much the agent is willing to rearrange consumption across time in response to anticipated changes in the return to saving. In the CRRA case $u(c) = c^{1-\gamma}/(1-\gamma)$, both are fully determined by $\gamma$: RRA $= \gamma$ and EIS $= 1/\gamma$.

The identification of these two conceptually distinct attributes in a single parameter is not a deep result — it is a consequence of the *temporal compound lottery axiom*, which requires that the agent is indifferent between resolving uncertainty now versus resolving it gradually over time. If the agent cares about the *timing* of resolution of uncertainty — if she prefers early resolution to late resolution, or vice versa — the expected utility framework cannot accommodate this preference. Recursive preferences can.

### The Atemporal vs. Intertemporal Tradeoff

Consider two stylized questions that capture the distinction:

**Risk aversion question**: Would you rather have a sure consumption level of $c$ or a 50/50 gamble between $\alpha c$ and $c/\alpha$ for some $\alpha > 1$, in a single period? The answer depends on RRA.

**EIS question**: If the real interest rate rises by 1%, by what percentage does your optimal consumption growth rate increase? The answer depends on EIS — a high EIS implies a strong reallocation of consumption toward the future.

These are two entirely different questions about two entirely different aspects of preferences. Standard expected utility answers both with the same parameter $\gamma$. Recursive preferences allow them to be answered independently.

---

## 2. The Epstein-Zin Preference Representation

### The Recursive Definition

Epstein and Zin (1989), building on Kreps and Porteus (1978), proposed the following recursive utility representation:

$$
U_t = \left[(1-\beta) c_t^{1-1/\psi} + \beta \left(\mathbb{E}_t\left[U_{t+1}^{1-\gamma}\right]\right)^{\frac{1-1/\psi}{1-\gamma}}\right]^{\frac{1}{1-1/\psi}}
$$

where $\gamma > 0$ is the coefficient of relative risk aversion, $\psi > 0$ is the elasticity of intertemporal substitution, and $\beta \in (0,1)$ is the subjective discount factor. When $\gamma = 1/\psi$ — when risk aversion equals the inverse of the EIS — this collapses exactly to standard power (CRRA) expected utility. In general, however, $\gamma$ and $\psi$ are free to take any positive values independently.

It is helpful to write this more compactly. Define $\rho = 1 - 1/\psi$ (the elasticity of the CES aggregator) and $\alpha = 1 - \gamma$ (the risk preference parameter). Then:

$$
U_t = \left[(1-\beta) c_t^{\rho} + \beta \left(\mathbb{E}_t\left[U_{t+1}^{\alpha}\right]\right)^{\rho/\alpha}\right]^{1/\rho}
$$

This is a **CES aggregator** over current consumption $c_t$ and a certainty equivalent of future utility, $\mu_t(U_{t+1}) = (\mathbb{E}_t[U_{t+1}^\alpha])^{1/\alpha}$. The certainty equivalent $\mu_t$ is a standard power mean with parameter $\alpha = 1 - \gamma$ — it captures the agent's attitude toward risk in future utility. The outer CES structure with parameter $\rho = 1 - 1/\psi$ captures the agent's willingness to substitute consumption across time.

### The Key Special Cases

Several limiting cases illuminate the structure:

**CRRA expected utility** ($\gamma = 1/\psi$): As noted, the Epstein-Zin form collapses to $U_t = \mathbb{E}_t[\sum_\tau \beta^\tau c_{t+\tau}^{1-\gamma}/(1-\gamma)]$ when risk aversion equals the reciprocal of EIS.

**Log utility** ($\gamma = 1, \psi = 1$): Utility is $U_t = (1-\beta)\ln c_t + \beta \mathbb{E}_t[U_{t+1}]$, collapsing to the standard log-utility specification.

**Risk-neutral agent** ($\gamma = 0$): The certainty equivalent is $\mu_t = \mathbb{E}_t[U_{t+1}]$ — the agent is indifferent to risk and only the expected future utility matters.

**Infinite EIS** ($\psi \to \infty$, $\rho \to 1$): Utility is linear in consumption: $U_t = (1-\beta)c_t + \beta(\mathbb{E}_t[U_{t+1}^\alpha])^{1/\alpha}$. The agent will perfectly smooth consumption across time — any deviation from a flat consumption path is infinitely costly — while still being averse to contemporaneous risk.

### Preference for Early vs. Late Resolution of Uncertainty

A fundamental property that distinguishes Epstein-Zin preferences from expected utility is their attitude toward the *timing* of resolution of uncertainty. Consider an agent who will learn tomorrow whether she will receive a high or low income stream for the rest of her life. Does she prefer to learn this today?

Under expected utility, the agent is **indifferent** to the timing of information revelation (this is the compound lottery axiom). Under Epstein-Zin preferences:

- If $\gamma > 1/\psi$ (RRA exceeds the reciprocal of EIS), the agent **prefers early resolution** of uncertainty. She would rather know bad news today than live in suspense.
- If $\gamma < 1/\psi$, the agent **prefers late resolution**. Ignorance is bliss — she would rather not know.

This preference for early versus late resolution of uncertainty has deep implications for asset pricing. An agent who prefers early resolution of uncertainty places extra value on assets that hedge against news about the long-run future — assets that pay off when long-run prospects deteriorate. Conversely, assets that are exposed to long-run risk command a premium. This is the channel that the long-run risk model of Block 3.4 will exploit.

---

## 3. The Epstein-Zin Stochastic Discount Factor

### Deriving the SDF

The SDF for Epstein-Zin preferences is the central result needed for asset pricing applications. It is derived from the agent's optimality conditions in a manner analogous to the CRRA case, but the recursive structure introduces an additional term.

Let $W_t$ denote the agent's total wealth — the present value of all future consumption. The **return on the wealth portfolio** is:

$$
R^W_{t+1} = \frac{W_{t+1}}{W_t - c_t}
$$

This is the gross return on the claim to all future consumption — the "market portfolio" in the Lucas economy where aggregate wealth equals the present value of the consumption endowment. Under market clearing, $R^W_{t+1}$ is the return on the aggregate wealth portfolio.

The Epstein-Zin SDF is:

$$
\boxed{m_{t+1} = \beta^\theta \left(\frac{c_{t+1}}{c_t}\right)^{-\theta/\psi} \left(R^W_{t+1}\right)^{\theta - 1}}
$$

where $\theta = (1-\gamma)/(1-1/\psi)$ is a composite parameter that governs the relative weight of the two components. When $\gamma = 1/\psi$ (expected utility), $\theta = 1$ and the wealth return term drops out, recovering the standard CRRA SDF.

Let us examine each component:

**The consumption growth term** $\beta^\theta (c_{t+1}/c_t)^{-\theta/\psi}$: This is the intertemporal substitution component. It appears because the agent is willing to substitute consumption across time — the SDF must price this substitution correctly. The exponent $\theta/\psi$ is the elasticity of the SDF with respect to consumption growth.

**The wealth return term** $(R^W_{t+1})^{\theta-1}$: This is the risk aversion component. It captures how the agent values aggregate wealth fluctuations beyond what is captured by current consumption growth alone. When $\theta > 1$ (which requires either $\gamma > 1$ and $\psi > 1$, or $\gamma < 1$ and $\psi < 1$), the SDF is decreasing in the wealth return — the agent dislikes states where the aggregate portfolio does poorly. When $\theta < 1$, the reverse holds.

**The two-component structure** is the defining characteristic of the Epstein-Zin SDF. Unlike the CRRA case where everything depends on consumption growth alone, the Epstein-Zin SDF depends on both consumption growth and aggregate wealth returns. This is not a minor refinement — it fundamentally changes what risks are priced and at what level.

### The Log-Linear SDF Approximation

For empirical work and calibration, it is useful to work with the log-linear approximation. Taking logs of the SDF:

$$
\ln m_{t+1} = \theta \ln\beta - \frac{\theta}{\psi} \Delta\ln c_{t+1} + (\theta-1)\ln R^W_{t+1}
$$

Under the log-normal approximation (assuming log consumption growth and log wealth returns are jointly normally distributed), the expected log SDF is:

$$
\mathbb{E}_t[\ln m_{t+1}] = \theta\ln\beta - \frac{\theta}{\psi}\mathbb{E}_t[\Delta\ln c_{t+1}] + (\theta-1)\mathbb{E}_t[\ln R^W_{t+1}] + \text{Jensen terms}
$$

The log risk-free rate is:

$$
r_{f,t} \approx -\theta\ln\beta + \frac{\theta}{\psi}\mathbb{E}_t[\Delta\ln c_{t+1}] - \frac{\theta^2}{2\psi^2}\sigma^2_c - \frac{(1-\theta)^2}{2}\sigma^2_{r^W} - \theta(1-\theta)\frac{1}{\psi}\text{Cov}_t(\Delta\ln c, \ln R^W)
$$

The first two terms give the familiar Ramsey rule ($r_f = \delta + g/\psi$, where $\delta = -\ln\beta$). The remaining terms are variance and covariance corrections that arise under log-normality. The key observation is that the EIS $\psi$ appears in the coefficient $1/\psi$ of mean consumption growth — so the relationship between $r_f$ and consumption growth is governed by EIS, not by risk aversion $\gamma$. This breaks the risk-free rate puzzle: with high $\psi$, the agent is willing to tolerate time variation in consumption growth without demanding large interest rate movements to compensate.

---

## 4. Why Epstein-Zin Matters: Resolving the Joint Puzzle

### The Decoupling

Under CRRA expected utility, the risk-free rate and the equity premium are both pinned by $\gamma$:

- **Risk-free rate**: $r_f \approx \delta + \gamma g - \frac{\gamma^2}{2}\sigma^2_c$. High $\gamma$ implies high $r_f$.
- **Equity premium**: $\mathbb{E}[r^{eq}] - r_f \approx \gamma \cdot \text{Cov}(\Delta\ln c, r^{eq})$. High $\gamma$ implies high premium.

These constraints are contradictory given observed data: a large equity premium requires high $\gamma$, but high $\gamma$ also implies a counterfactually high risk-free rate. With a single parameter, there is no escape.

Under Epstein-Zin preferences:

- **Risk-free rate**: $r_f \approx \delta + g/\psi + \ldots$. The risk-free rate is governed by EIS $\psi$.
- **Equity premium**: The premium reflects both $\gamma$ (through the SDF's sensitivity to consumption growth) and $\theta$ (through the wealth return component). With $\gamma > 1/\psi$ and $\theta > 1$, the equity premium can be large even when $\psi$ is large.

With $\gamma = 10$ and $\psi = 1.5$, for example:
- The EIS of $1.5$ implies moderate consumption growth sensitivity to interest rates — the agent smooths across time without extreme reluctance.
- The RRA of $10$ implies substantial aversion to contemporaneous risk — the agent demands significant premia for bearing uncertainty.
- The risk-free rate is governed by EIS and remains close to its observed level.
- The equity premium is governed by RRA and can be large.

The joint equity premium and risk-free rate puzzle is, in principle, resolved by the decoupling. This was the fundamental motivation for Epstein and Zin's generalization, and it is why recursive preferences became the dominant paradigm in the consumption-based asset pricing literature following Bansal and Yaron (2004).

### The Quantitative Requirements

How large do $\gamma$ and $\psi$ need to be? Returning to the HJ bound: the required SDF volatility is $\sigma(m)/\mathbb{E}[m] \geq 0.5$. Under Epstein-Zin with the log-linear SDF:

$$
\frac{\sigma(m)}{\mathbb{E}[m]} \approx \sqrt{\left(\frac{\theta}{\psi}\right)^2 \sigma^2_c + (1-\theta)^2 \sigma^2_{r^W} + 2\frac{\theta}{\psi}(1-\theta)\text{Cov}(\Delta\ln c, \ln R^W)}
$$

With standard consumption growth volatility $\sigma_c \approx 1\%$ and wealth return volatility $\sigma_{r^W} \approx 15\%$, even moderate values of $\theta$ can generate sufficient SDF volatility through the wealth return component — provided the wealth return is sufficiently volatile and correlated with the bad states of the world. But this shifts the burden: the model needs to generate high wealth return volatility, which itself requires understanding what drives fluctuations in the price of the wealth portfolio. This is precisely the question that the long-run risk model of Block 3.4 answers.

---

## 5. The Role of the Wealth Portfolio Return

The appearance of $R^W_{t+1}$ in the Epstein-Zin SDF introduces a fundamental challenge for empirical work: the wealth portfolio — the claim to all future consumption — is not directly observable. Unlike the consumption-CAPM, where the SDF depends only on consumption growth (a NIPA aggregate), the Epstein-Zin SDF requires knowledge of the return on aggregate wealth including human capital, private businesses, real estate, and all other claims to future consumption.

### Approximating the Wealth Return

Several approaches have been used to proxy for $R^W$:

**The CRSP value-weighted stock market return**: The most common proxy in the literature. Justified if financial wealth is proportional to total wealth — a reasonable approximation if the non-financial components of wealth move closely with financial wealth.

**The cay variable** (Lettau and Ludvigson, 2001): Rather than directly measuring $R^W$, Lettau and Ludvigson construct a proxy for the log consumption-wealth ratio, which theory implies is a sufficient statistic for the expected wealth return. Since $R^W$ is the return on the consumption claim, its conditional expectation is related to the consumption-wealth ratio. The cay variable exploits this relationship and has been used as a conditioning variable to reveal time-varying risk premia.

**The human wealth return**: Lustig, Van Nieuwerburgh, and Verdelhan (2013) and others have constructed estimates of the return on human capital from labor income data. Including human wealth substantially changes the properties of the aggregate wealth portfolio, since human capital accounts for 60–70% of total wealth.

The dependence on an unobservable wealth return is a genuine challenge for the Epstein-Zin framework. It means the model is always estimated under a joint hypothesis about the form of preferences and the measurement of the wealth portfolio. This is analogous to the Roll critique in the CAPM — but the unobservability problem is somewhat less severe, since consumption data provides partial information about the wealth return.

### The Campbell (1993) Approximation

Campbell (1993) derived a log-linear approximation that expresses the Epstein-Zin SDF in terms of observable quantities — current and future consumption growth — by substituting the approximate present value relationship for the wealth return. The result is:

$$
\ln m_{t+1} \approx \text{const} - \frac{1}{\psi}\Delta\ln c_{t+1} - \left(\gamma - \frac{1}{\psi}\right)\sum_{j=1}^{\infty} \rho^j_c \mathbb{E}_{t+1}[\Delta\ln c_{t+1+j}] + \ldots
$$

The key term is the sum of future expected consumption growth rates, discounted at rate $\rho_c$. This is the **revision in expectations about long-run consumption growth** — the news about the future that arrives at $t+1$. When $\gamma > 1/\psi$ (so the coefficient on the revision term is negative), an upward revision in long-run growth prospects **reduces** the SDF — good long-run news is associated with low marginal utility and high discount rates. This is the "long-run risk" channel: assets that are exposed to deteriorations in long-run growth prospects are risky and command a premium.

This approximation is the theoretical foundation for the long-run risk model. It shows that with Epstein-Zin preferences and $\gamma > 1/\psi$, news about the long-run future is priced *separately* from news about current consumption. The SDF responds to two components of innovation: the short-run consumption shock (current news) and the long-run revision (news about the future). Assets correlated with the latter command their own risk premium — proportional to $(\gamma - 1/\psi)$, the departure from expected utility.

---

## 6. The Risk-Return Tradeoff Under Recursive Preferences

### The Price of Risk

Under Epstein-Zin preferences, the expected excess return on any asset can be decomposed using the log-linear SDF:

$$
\mathbb{E}_t[r^i_{t+1} - r_{f,t}] + \frac{\sigma^2_i}{2} = \underbrace{\frac{\theta}{\psi}\text{Cov}_t(\Delta\ln c_{t+1}, r^i_{t+1})}_{\text{Short-run consumption risk}} + \underbrace{(1-\theta)\text{Cov}_t(\ln R^W_{t+1}, r^i_{t+1})}_{\text{Wealth return risk}}
$$

This is the Epstein-Zin version of the beta pricing formula. Expected excess returns depend on two covariances: the covariance with contemporaneous consumption growth (the short-run channel) and the covariance with the wealth return (the intertemporal channel). When $\theta = 1$ (expected utility), the second term vanishes and we recover the standard C-CAPM. When $\theta \neq 1$, both channels contribute.

The two channels capture fundamentally different sources of risk:

**Short-run consumption risk** is the familiar CCAPM risk: assets that pay off poorly when current consumption is low are undesirable and command a premium proportional to $\theta/\psi$.

**Wealth return risk** captures the risk of changes in investment opportunities. Assets that fall in value when the aggregate portfolio falls (the wealth effect) are risky in a way that goes beyond current consumption. The coefficient $(1-\theta)$ can be large when $\gamma$ and $\psi$ differ substantially, making this channel empirically important.

### Long-Horizon Risk Pricing

A profound implication of recursive preferences is that **long-horizon risks are priced separately from short-horizon risks**. An asset that pays off poorly in periods of low *future* consumption growth — not just current consumption growth — is risky under Epstein-Zin preferences when $\gamma > 1/\psi$. The agent's preference for early resolution of uncertainty means she places extra weight on news about the future, making long-run exposure a genuine source of systematic risk.

This can be seen directly from the Campbell (1993) approximation: the Epstein-Zin SDF responds to revisions in expectations about all future consumption growth rates, not just current consumption growth. In contrast, the CRRA SDF only responds to current consumption growth — it has no memory and no foresight beyond the immediate period.

This is a fundamental generalization. It means that assets with different **long-run beta profiles** — different exposures to long-horizon consumption risk — can have different expected returns even if their current-period betas are identical. Two assets might have the same covariance with current consumption growth, the same exposure to the market return, and yet different expected returns under Epstein-Zin preferences if they differ in their exposure to revisions in long-run growth expectations. Empirically, this generates return dispersion that neither the CAPM nor the standard C-CAPM can explain.

---

## 7. Empirical Evidence on Recursive Preferences

### The EIS: Estimation and Debate

The empirical evidence on the EIS is surprisingly unsettled given its centrality to the recursive preference framework. Early estimates by Hall (1988) using aggregate consumption data found EIS estimates close to zero — suggesting that consumption growth barely responds to interest rate changes, inconsistent with the high EIS values needed for the long-run risk model. This finding implied $\psi \approx 0.1$, far below the $\psi > 1$ values that Bansal and Yaron (2004) require.

However, Hall's approach — regressing consumption growth on the real interest rate — is subject to severe identification problems. The real interest rate and consumption growth are both endogenous, driven by the same underlying shocks, making OLS estimates biased. Subsequent work using instrumental variable approaches (Attanasio and Weber, 1993), cross-country data (Ogaki and Reinhart, 1998), and stock market returns as instruments (Vissing-Jørgensen, 2002) has found EIS estimates ranging from $0.3$ to $1.5$, with the balance of the evidence suggesting $\psi > 0.5$ and quite possibly $\psi > 1$.

The most direct evidence comes from Bansal, Kiku, and Yaron (2012), who structurally estimate the long-run risk model and find EIS estimates around $1.5$–$2.0$ — comfortably above one and consistent with the model's requirements. This is the value that makes the long-run risk channel quantitatively important, as we will see in Block 3.4.

### Portfolio Implications

Recursive preferences have notable implications for portfolio choice that distinguish them from the CRRA case:

**Hedging demands**: Under CRRA utility, optimal portfolio weights are myopic — the investor holds the same portfolio in every period, regardless of the current state of the world. Under Epstein-Zin preferences with $\psi \neq 1/\gamma$, there are **intertemporal hedging demands**: the investor holds assets not only for their immediate risk-return tradeoff but also to hedge against future changes in the investment opportunity set. This is the Merton (1973) ICAPM in action, but now derived from first principles of recursive preferences rather than assumed.

**The equity-bond allocation**: The optimal allocation between stocks and bonds under Epstein-Zin preferences depends on both risk aversion (which determines the unconditional equity allocation) and EIS (which governs the response to interest rate changes and shifts in expected returns). An investor with high $\psi$ adjusts her portfolio aggressively in response to predictable variation in equity premia — she tilts heavily toward equities when expected returns are high, consistent with value-timing strategies.

**The preference for early resolution and bond pricing**: An agent with $\gamma > 1/\psi$ who prefers early resolution of uncertainty demands a positive term premium on long-maturity bonds: they expose the agent to uncertainty about long-run interest rates and inflation, precisely the type of long-horizon risk that is separately priced under recursive preferences. This generates a richer term structure than the standard expectations hypothesis.

---

## 8. The Relationship Between Recursive Preferences and Habit Formation

Recursive preferences and habit formation are often presented as competing resolutions to the equity premium puzzle. They share the goal of generating a more volatile SDF at plausible parameter values, but they do so through fundamentally different mechanisms:

**Habit formation** achieves SDF volatility by making the agent's *current* marginal utility highly state-dependent — it amplifies the response of marginal utility to current consumption fluctuations by placing the agent close to the habit threshold. The SDF is volatile because any small decline in current consumption triggers a large increase in current marginal utility.

**Recursive preferences** achieve SDF volatility primarily through sensitivity to *news about the future*. With high $\gamma > 1/\psi$, the agent cares intensely about revisions in long-run expectations — small persistent signals about future consumption growth cause large swings in the pricing kernel. The SDF is volatile not because current consumption is volatile but because the agent reacts strongly to information about the long-run.

This distinction has important empirical implications. Habit formation predicts that risk premia are driven by the *level* of the surplus consumption ratio — a function of past consumption history. Recursive preferences predict that risk premia are driven by innovations to *expected future consumption growth* — a forward-looking variable. These two predictions can in principle be separately tested, and the evidence suggests that both channels are likely operative: the habit literature documents backward-looking predictors of risk premia (cay as a proxy for the surplus ratio), while the long-run risk literature documents forward-looking predictors (variables that forecast long-run consumption growth).

An important practical distinction is that the Campbell-Cochrane model achieves its results with $\gamma = 2$ and $\psi = 0.5$, while the Bansal-Yaron model requires $\gamma \approx 10$ and $\psi \approx 1.5$. The former implies very low fundamental risk aversion amplified by the habit mechanism; the latter implies moderate-to-high risk aversion combined with high intertemporal substitution. Empirically distinguishing these cases requires identifying the independent variation in risk aversion and EIS — a challenging task but one that the literature has made substantial progress on.

---

## 9. The SDF Volatility Decomposition

A clean way to see what Epstein-Zin preferences add over CRRA is to decompose the SDF variance:

$$
\text{Var}(\ln m_{t+1}) = \underbrace{\left(\frac{\theta}{\psi}\right)^2 \sigma^2_c}_{\text{Short-run consumption}} + \underbrace{(1-\theta)^2 \sigma^2_{r^W}}_{\text{Wealth return}} + \underbrace{2\frac{\theta}{\psi}(1-\theta)\text{Cov}(\Delta\ln c, r^W)}_{\text{Cross term}}
$$

With $\sigma_c \approx 1\%$, $\sigma_{r^W} \approx 15\%$, $\gamma = 10$, $\psi = 1.5$:
- $\theta = (1-10)/(1-1/1.5) = -9/(1/3) = -27$
- Short-run term: $(\theta/\psi)^2 \sigma^2_c = (-18)^2 \cdot (0.01)^2 \approx 0.032$
- Wealth return term: $(1-\theta)^2 \sigma^2_{r^W} = (28)^2 \cdot (0.15)^2 \approx 17.6$

The wealth return term dominates overwhelmingly. This is the key: the SDF volatility under Epstein-Zin is driven primarily by aggregate wealth return fluctuations, not by consumption growth. This dramatically relaxes the constraint on consumption smoothness — even very smooth consumption is consistent with a volatile SDF, provided the aggregate portfolio is sufficiently volatile and exposed to the relevant sources of risk.

This is the HJ bound satisfied not by making consumption more volatile or risk aversion implausibly high, but by recognizing that the pricing kernel under recursive preferences has a rich dependence on aggregate wealth dynamics that the CRRA model ignores entirely.

---

## Key Takeaways

**Recursive preferences disentangle risk aversion $\gamma$ from the elasticity of intertemporal substitution $\psi$.** Under CRRA expected utility, $EIS = 1/\gamma$ — a constraint that makes the equity premium puzzle and the risk-free rate puzzle jointly irreconcilable. Epstein-Zin preferences break this constraint.

**The Epstein-Zin SDF has two components:** a consumption growth term (governing intertemporal substitution) and a wealth return term (governing the pricing of aggregate risk). The relative weight between them is controlled by $\theta = (1-\gamma)/(1-1/\psi)$.

**With $\gamma > 1/\psi$, the agent prefers early resolution of uncertainty**, making her sensitive to news about the long-run future. Assets that covary negatively with revisions to long-run growth expectations are risky and command a premium — even if their exposure to current consumption risk is modest. This is the long-run risk channel.

**The risk-free rate is governed by EIS, not risk aversion.** A high $\psi$ keeps the risk-free rate low and stable even with high $\gamma$, resolving the joint equity premium and risk-free rate puzzle.

**SDF volatility under Epstein-Zin is dominated by wealth return fluctuations**, not consumption growth volatility. This satisfies the HJ bound without requiring implausibly high $\gamma$ or implausibly volatile consumption — the pricing kernel's volatility comes from aggregate wealth dynamics.

**Recursive preferences and habit formation are complementary, not competing.** Habit achieves SDF volatility through state-dependent current marginal utility; recursive preferences achieve it through sensitivity to long-run news. Both channels appear to be empirically operative, and they make distinct, testable predictions about the sources and timing of risk premia.

---

## Looking Ahead: Block 3.4 — Long-Run Risk

Block 3.3 established that recursive preferences make the agent sensitive to news about the long-run future — that with $\gamma > 1/\psi$, revisions in expected long-run consumption growth are priced risks. Block 3.4 exploits this insight fully. Bansal and Yaron (2004) introduced a small but persistent predictable component in consumption growth — "long-run risk" — and showed that even tiny fluctuations in long-run expected growth can generate large risk premia when combined with Epstein-Zin preferences and high EIS. The model simultaneously matches the equity premium, the risk-free rate, the volatility of stock returns, the predictability of returns, and the behavior of the price-dividend ratio — a remarkable breadth of empirical success. We will derive the model's key results, examine its calibration and its tension with consumption data, and assess its contribution to the resolution of the equity premium puzzle.

---

*Block 3.2 — Habit Formation | **Block 3.3 — Recursive Preferences** | Block 3.4 — Long-Run Risk →*
