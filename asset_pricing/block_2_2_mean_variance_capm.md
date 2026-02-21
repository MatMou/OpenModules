# Block 2.2 — The Mean-Variance Frontier and the CAPM

> *"The basic idea is that investors should care about not just the expected return of a portfolio, but also its risk — measured by variance. This simple observation, combined with competitive equilibrium, generates one of the most important models in all of economics."*
> — Robert Merton, *Continuous-Time Finance* (1990)

---

## Where We Left Off

Block 2.1 established the SDF as the universal language of asset pricing. Every valid pricing model is a theory of $m$, and every asset's expected excess return is determined by its covariance with $m$. We also noted that the CAPM is the special case where $m = a - b \cdot R^{mkt}$ — a linear function of the market return. 

But *why* should the market return be the right factor? Under what conditions does a single beta with respect to the market portfolio suffice to explain all cross-sectional differences in expected returns? And what is the connection between the SDF and the mean-variance frontier that investors care about when constructing portfolios?

This block answers these questions from the ground up. We derive the mean-variance frontier geometrically and algebraically, establish its deep connection to the SDF, and then use that connection to derive the CAPM with full rigor — both in its classical form and in the more general SDF-based form that reveals exactly where and why the model can fail.

---

## 1. The Portfolio Problem: Means, Variances, and Diversification

### Setup

Consider $N$ risky assets with return vector $\mathbf{R} = (R_1, \ldots, R_N)'$, expected return vector $\boldsymbol{\mu} = \mathbb{E}[\mathbf{R}]$, and covariance matrix $\boldsymbol{\Sigma} = \text{Cov}(\mathbf{R})$, which we assume to be positive definite (no redundant assets). A portfolio is a vector of weights $\mathbf{w} = (w_1, \ldots, w_N)'$ with $\mathbf{w}'\mathbf{1} = 1$. The portfolio return is $R_p = \mathbf{w}'\mathbf{R}$, with:

$$
\mu_p = \mathbf{w}'\boldsymbol{\mu}, \qquad \sigma_p^2 = \mathbf{w}'\boldsymbol{\Sigma}\mathbf{w}
$$

### The Minimum-Variance Frontier

The **minimum-variance frontier** is the set of portfolios that achieve the lowest possible variance for each level of expected return. Formally, for each target $\bar{\mu}$, we solve:

$$
\min_{\mathbf{w}} \; \frac{1}{2} \mathbf{w}'\boldsymbol{\Sigma}\mathbf{w} \quad \text{subject to} \quad \mathbf{w}'\boldsymbol{\mu} = \bar{\mu}, \quad \mathbf{w}'\mathbf{1} = 1
$$

The Lagrangian is:

$$
\mathcal{L} = \frac{1}{2}\mathbf{w}'\boldsymbol{\Sigma}\mathbf{w} - \lambda(\mathbf{w}'\boldsymbol{\mu} - \bar{\mu}) - \gamma(\mathbf{w}'\mathbf{1} - 1)
$$

The first-order condition gives $\boldsymbol{\Sigma}\mathbf{w} = \lambda\boldsymbol{\mu} + \gamma\mathbf{1}$, so the optimal weight vector is:

$$
\mathbf{w}^* = \lambda \boldsymbol{\Sigma}^{-1}\boldsymbol{\mu} + \gamma \boldsymbol{\Sigma}^{-1}\mathbf{1}
$$

Imposing the two constraints to solve for $\lambda$ and $\gamma$ yields the key result: **every frontier portfolio is a linear combination of any two distinct frontier portfolios**. This is the celebrated **two-fund separation theorem**.

Define the two canonical frontier portfolios:
- $\mathbf{g}$: the global minimum-variance (GMV) portfolio — the portfolio with the lowest possible variance, regardless of expected return.
- $\mathbf{d}$: any other frontier portfolio (often chosen to have unit expected return or some other convenient normalization).

Then every frontier portfolio can be written as $\alpha \mathbf{g} + (1-\alpha)\mathbf{d}$ for some scalar $\alpha$. In $(\sigma, \mu)$ space, the frontier traces out a **hyperbola** — narrow at the GMV portfolio and opening upward and downward. The upper branch (above the GMV portfolio) is called the **efficient frontier**: the portfolios that are not dominated in mean-variance terms. No rational mean-variance investor would hold a portfolio on the lower branch, since it offers the same variance for a lower expected return.

### The Geometry of Diversification

The shape of the frontier reveals the power of diversification. To see this starkly, consider $N$ assets each with expected return $\mu$, variance $\sigma^2$, and pairwise correlation $\rho$. The equally-weighted portfolio has:

$$
\sigma_p^2 = \frac{\sigma^2}{N} + \frac{N-1}{N} \rho \sigma^2 \xrightarrow{N \to \infty} \rho \sigma^2
$$

As the number of assets grows, the idiosyncratic variance $\sigma^2/N$ vanishes, but the **systematic variance** $\rho\sigma^2$ — the part that is common across assets — remains. This is the mathematical foundation of the intuition that only systematic risk is priced: diversification eliminates idiosyncratic variance for free, so the market charges no premium for it. Only the residual, undiversifiable systematic risk deserves compensation.

---

## 2. Adding the Risk-Free Asset: The Capital Market Line

Now introduce a risk-free asset with return $R_f$. An investor can combine any risky portfolio $p$ with the risk-free asset. If the fraction $\alpha$ is invested in portfolio $p$ and $(1-\alpha)$ in the risk-free asset:

$$
\mu = \alpha \mu_p + (1-\alpha) R_f = R_f + \alpha(\mu_p - R_f)
$$
$$
\sigma = \alpha \sigma_p
$$

Eliminating $\alpha$: $\mu = R_f + \frac{\mu_p - R_f}{\sigma_p} \cdot \sigma$. This is a **straight line** in $(\sigma, \mu)$ space emanating from the risk-free asset $(0, R_f)$ with slope $(\mu_p - R_f)/\sigma_p$ — the Sharpe ratio of portfolio $p$.

The investor wants to maximize this slope — to reach the steepest possible line from $R_f$. The optimal risky portfolio is the one where this line is **tangent** to the risky asset frontier. This tangency portfolio $T$ is:

$$
\mathbf{w}^T = \frac{\boldsymbol{\Sigma}^{-1}(\boldsymbol{\mu} - R_f \mathbf{1})}{\mathbf{1}'\boldsymbol{\Sigma}^{-1}(\boldsymbol{\mu} - R_f \mathbf{1})}
$$

and the **Capital Market Line (CML)** is:

$$
\mu_p = R_f + \frac{\mu_T - R_f}{\sigma_T} \cdot \sigma_p
$$

This is a fundamental insight: every mean-variance investor — regardless of risk aversion — holds the same risky portfolio $T$, combined with the risk-free asset in proportions that depend on individual risk tolerance. A more risk-averse investor holds more in the risk-free asset; a less risk-averse investor levers up by borrowing at $R_f$ and investing more than $100\%$ in $T$. But the composition of the risky portion is universal. This is **two-fund separation** in its sharpest form.

---

## 3. The Connection Between the Frontier and the SDF

Here we establish the central mathematical result that links mean-variance analysis to the SDF — a result that is beautiful in its symmetry and powerful in its implications.

**Theorem (Frontier-SDF Duality)**: A return $R^{mv}$ is on the mean-variance frontier of risky assets if and only if $R^{mv}$ can serve as the basis of a valid SDF. More precisely:

- If $m = a + b \cdot R^{mv}$ for constants $a$ and $b$ with $b \neq 0$, then $m$ prices all assets in $\mathcal{X}$.
- Conversely, if $m$ prices all assets, then the projection of $m$ onto the space of asset returns, $m^* = \text{proj}(m | \mathcal{X})$, corresponds to a frontier portfolio.

**Proof sketch**: Any valid SDF $m$ must satisfy $1 = \mathbb{E}[mR^i]$ for all $i$. The minimum-variance SDF $m^*$ is the element of $\mathcal{X}$ that achieves this — it is the projection of $m$ onto the payoff space. One can show that $m^*$ is a linear function of asset returns if and only if it lies on the mean-variance frontier of those returns. The correspondence is exact: every frontier portfolio $R^{mv}$ yields an SDF $m = a + bR^{mv}$ that prices assets correctly, and every minimum-variance SDF corresponds to a frontier return.

This duality means that **mean-variance efficiency and SDF validity are two descriptions of the same mathematical object**. When we ask "is the market portfolio mean-variance efficient?", we are asking exactly the same question as "is $m = a - b R^{mkt}$ a valid SDF?" — which is exactly the CAPM.

The practical implication is powerful: any test of whether a portfolio is mean-variance efficient is simultaneously a test of the factor model generated by that portfolio, and vice versa. The empirical literature on the CAPM and its tests becomes unified under this lens.

---

## 4. Deriving the CAPM

Armed with the frontier-SDF duality, we can derive the CAPM with remarkable concision. There are several derivation strategies; we present the three most illuminating.

### Derivation 1: The Equilibrium Argument (Sharpe-Lintner)

Assume:
1. All investors have mean-variance preferences (or equivalently, returns are jointly normal and investors maximize expected utility).
2. All investors face the same risk-free rate $R_f$ and have **homogeneous beliefs** — they agree on $\boldsymbol{\mu}$ and $\boldsymbol{\Sigma}$.
3. Markets clear: supply equals demand for every asset.

By two-fund separation, every investor holds the tangency portfolio for their risky allocation. When all investors hold the same risky portfolio and markets clear, the tangency portfolio must equal the **market portfolio** $R^{mkt}$ — the value-weighted portfolio of all risky assets. (If any asset were over- or under-held relative to its market weight, prices would adjust until investors are content to hold market weights.)

The CML applies to the market portfolio:

$$
\mu_{mkt} - R_f = \frac{\mu_{mkt} - R_f}{\sigma_{mkt}} \cdot \sigma_{mkt}
$$

For any individual asset $i$, the tangency condition implies:

$$
\mu_i - R_f = \beta_i \left(\mu_{mkt} - R_f\right)
$$

where $\beta_i = \text{Cov}(R^i, R^{mkt})/\text{Var}(R^{mkt})$. This is the **Security Market Line (SML)** — the CAPM.

### Derivation 2: The SDF Argument

By the frontier-SDF duality, if the market portfolio is mean-variance efficient, then $m = a + b R^{mkt}$ is a valid SDF for some constants $a$ and $b$. The expected return equation $\mathbb{E}[R^i] - R_f = -R_f \text{Cov}(m, R^i)$ then gives:

$$
\mathbb{E}[R^i] - R_f = -R_f b \cdot \text{Cov}(R^{mkt}, R^i)
$$

Applying this to the market itself:

$$
\mathbb{E}[R^{mkt}] - R_f = -R_f b \cdot \text{Var}(R^{mkt})
$$

so $-R_f b = (\mathbb{E}[R^{mkt}] - R_f)/\text{Var}(R^{mkt})$. Substituting:

$$
\mathbb{E}[R^i] - R_f = \frac{\text{Cov}(R^{mkt}, R^i)}{\text{Var}(R^{mkt})} \cdot \left(\mathbb{E}[R^{mkt}] - R_f\right) = \beta_i \cdot \left(\mathbb{E}[R^{mkt}] - R_f\right)
$$

The CAPM follows immediately from the market portfolio being mean-variance efficient — without any explicit assumption about investor preferences beyond mean-variance.

### Derivation 3: The Zero-Beta CAPM (Black, 1972)

What if there is no risk-free asset? Black showed that the CAPM still holds in a modified form. Every frontier portfolio $p$ has a unique **zero-beta portfolio** $z(p)$ — the frontier portfolio with zero covariance with $p$:

$$
\text{Cov}(R^p, R^{z(p)}) = 0
$$

The zero-beta return $\mathbb{E}[R^{z(p)}]$ plays the role of the risk-free rate. The Black CAPM is:

$$
\mathbb{E}[R^i] = \mathbb{E}[R^{z(mkt)}] + \beta_i \left(\mathbb{E}[R^{mkt}] - \mathbb{E}[R^{z(mkt)}]\right)
$$

This version is important because it holds even when borrowing at the risk-free rate is restricted or unavailable — a realistic assumption for many institutional investors. Empirically, the zero-beta return tends to be *above* the Treasury bill rate, which the standard CAPM predicts should be zero — consistent with limits to arbitrage preventing investors from fully equalizing borrowing and lending rates.

---

## 5. The Security Market Line: Geometry and Interpretation

The Security Market Line deserves careful attention. It is the cross-sectional prediction of the CAPM: plotted in $(\beta, \mu)$ space, all assets and portfolios should lie on the straight line:

$$
\mu_i = R_f + \beta_i (\mu_{mkt} - R_f)
$$

A few observations:

**The SML is about systematic risk only.** An asset with high variance but low beta (high idiosyncratic risk, low market covariance) earns only a modest expected return. An asset with low variance but high beta earns a high expected return. It is the beta — the sensitivity to market-wide fluctuations — that is compensated, not variance per se.

**Alpha is the vertical deviation from the SML.** The **Jensen's alpha** of an asset is:

$$
\alpha_i = \mathbb{E}[R^i] - R_f - \beta_i(\mathbb{E}[R^{mkt}] - R_f)
$$

Under the CAPM, $\alpha_i = 0$ for all assets in equilibrium. A positive alpha means the asset earns more than its systematic risk justifies — it plots above the SML. In the world of the CAPM, persistent positive alphas cannot exist: investors would buy the asset, driving up its price and reducing its expected return until alpha returns to zero.

**The CML vs. the SML** are often confused but measure different things. The CML plots portfolios on the efficient frontier in $(\sigma, \mu)$ space; it applies to *efficient* portfolios only. The SML plots all assets and portfolios in $(\beta, \mu)$ space; it applies universally, including to individual stocks and inefficient portfolios. An individual stock generally plots inside the CML (it is not efficient) but on the SML (it correctly prices systematic risk).

---

## 6. Assumptions and Failures of the CAPM

The CAPM rests on a set of assumptions that are, to varying degrees, violated in practice. A mature understanding of the model requires knowing exactly which assumptions drive which results — and what happens when they fail.

### The Assumptions

The Sharpe-Lintner CAPM requires: (1) mean-variance preferences or normally distributed returns; (2) homogeneous beliefs; (3) a single investment period; (4) frictionless markets with unrestricted borrowing and lending at $R_f$; and (5) all assets are tradable and held in the market portfolio.

Each assumption has known failure modes:

**Heterogeneous beliefs**: If investors disagree about $\boldsymbol{\mu}$ or $\boldsymbol{\Sigma}$, the aggregation argument breaks down — different investors hold different tangency portfolios. The market portfolio need not be the mean-variance efficient portfolio for any individual investor. Models with heterogeneous beliefs (e.g., Harrison and Kreps, 1978; Scheinkman and Xiong, 2003) generate speculative premia and excessive trading volume, phenomena absent from the standard CAPM.

**Non-normal returns**: Equity returns exhibit fat tails (kurtosis), negative skewness, and time-varying volatility. Under non-normality, variance is no longer a complete description of risk: investors also care about higher moments. Kraus and Litzenberger (1976) showed that a co-skewness term enters the pricing equation when agents have three-moment preferences. More generally, assets with negative co-skewness with the market (they fall sharply when the market falls sharply) carry a premium beyond that implied by beta alone.

**Multiple periods**: In a multi-period world, investors must hedge against changes in the investment opportunity set — against shifts in expected returns, volatilities, and correlations. Merton's (1973) Intertemporal CAPM (ICAPM) shows that the pricing equation gains additional terms for each "state variable" that drives investment opportunities. This provides a theoretical foundation for multi-factor models: each Merton hedge portfolio against a state variable becomes an additional pricing factor.

**Non-tradable assets**: Human capital — the present value of future labor income — is typically the largest component of individual wealth, yet it is not directly tradable. If labor income risk is correlated with market returns (as it is for many individuals), the true "market portfolio" should include human capital. Mayers (1972) derived the CAPM with non-tradable assets, showing that the relevant covariance is with the full wealth portfolio including human capital, not just financial wealth.

**Borrowing constraints**: When investors cannot borrow freely at $R_f$, the zero-beta version applies and the SML is flatter than the standard CAPM predicts. The empirical literature consistently finds that the SML is too flat — low-beta stocks earn more than the CAPM predicts, and high-beta stocks earn less. This "betting against beta" anomaly (Frazzini and Pedersen, 2014) is quantitatively consistent with leverage constraints.

### The Roll Critique

Perhaps the most fundamental criticism of the CAPM is due to Richard Roll (1977). Roll showed that:

1. The only testable implication of the CAPM is that the market portfolio is mean-variance efficient.
2. The true market portfolio includes *all* assets — stocks, bonds, real estate, human capital, private businesses, and so on — and is never directly observable.
3. Tests of the CAPM using a proxy for the market portfolio (e.g., the S&P 500) test whether the *proxy* is efficient, not whether the *true* market portfolio is efficient. A rejection could reflect either a true failure of the CAPM or simply a poor proxy.

This is not merely an econometric observation — it is a conceptual one. The CAPM is a statement about an unobservable object. Every empirical test is therefore a joint test of the model and the market proxy used. This observation motivated the development of the APT and multi-factor models, which we turn to in Block 2.3, as more robust and testable alternatives.

---

## 7. Empirical Evidence: What Does the Data Say?

The CAPM was one of the most actively tested models in finance from the 1960s through the 1990s. The broad verdict is that the model contains important truth but is quantitatively insufficient.

### Early Support

Early tests by Black, Jensen, and Scholes (1972) and Fama and MacBeth (1973) found that the cross-section of expected returns was roughly linear in market beta, as the CAPM predicts. The SML appeared to have the right slope — beta explained a significant fraction of the variation in average returns across portfolios.

### The Anomalies

Subsequent evidence revealed systematic departures from the CAPM that are too large and too persistent to dismiss as sampling error:

**The size effect** (Banz, 1981): Small-cap stocks earn higher average returns than their betas imply. The difference is substantial — roughly 3–5% per annum on an annualized basis after controlling for beta.

**The value effect** (Rosenberg, Reid, and Lanstein, 1985; Fama and French, 1992): Stocks with high book-to-market ratios ("value stocks") earn higher average returns than growth stocks, controlling for beta. The value premium has been documented across countries and time periods.

**The momentum effect** (Jegadeesh and Titman, 1993): Stocks that have performed well over the past 6–12 months continue to outperform over the next 6–12 months. Momentum is among the strongest and most robust anomalies in finance, and it cannot be explained by beta.

**The low-beta anomaly**: As noted, high-beta stocks earn less than the CAPM predicts and low-beta stocks earn more. The empirical SML is significantly flatter than theory dictates.

These anomalies do not definitively falsify the CAPM — they could reflect the Roll critique, data mining, or risk factors that a properly specified market portfolio would capture. But they motivated the development of multi-factor models, beginning with Fama and French (1993), which we develop in Block 2.3.

---

## 8. The CAPM as a Special Case of the SDF Framework

Let us close by placing everything within the SDF language developed in Block 2.1 — making explicit what the CAPM adds to and assumes within the general framework.

The general pricing equation is $1 = \mathbb{E}[mR]$ for any valid SDF $m > 0$. The CAPM asserts the specific parametric form:

$$
m = a - b \cdot R^{mkt}, \quad a, b > 0
$$

For this to be a valid SDF, we need $m > 0$ in all states — which requires that $a > b \cdot R^{mkt,s}$ for all states $s$. Under normality, this holds almost everywhere for appropriate $a$ and $b$. Under non-normality (fat tails, crashes), there exist states where $R^{mkt}$ is so extreme that a linear $m$ becomes negative — a violation of no-arbitrage. This is the root of the CAPM's failure under non-normal returns.

The frontier-SDF duality tells us exactly what "market portfolio efficiency" means in SDF language: it means that the true SDF lies in the space spanned by the risk-free payoff and the market return. Any additional risk factors — size, value, momentum, liquidity — that are priced in the data are evidence that the true SDF requires additional dimensions beyond the market return alone.

From this vantage point, the anomalies and the multifactor literature are not a rejection of the SDF framework — they are a refinement of our understanding of what $m$ looks like. The CAPM told us $m$ is linear in the market. Fama-French tells us we need value and size factors too. Momentum adds another. The quest for the true SDF continues — and it is precisely what empirical asset pricing is about.

---

## Key Takeaways

**The mean-variance frontier is the set of portfolios with minimum variance for each level of expected return.** With a risk-free asset, every investor holds the tangency portfolio combined with the risk-free asset. The tangency portfolio is the unique portfolio that maximizes the Sharpe ratio.

**Every frontier portfolio corresponds to a valid SDF, and vice versa.** Mean-variance efficiency and SDF validity are mathematically equivalent. Testing whether the market portfolio is efficient is testing the CAPM's specific form of the SDF.

**The CAPM follows from market clearing under homogeneous beliefs and mean-variance preferences.** In equilibrium, the tangency portfolio equals the market portfolio. Expected returns are linear in market beta: $\mathbb{E}[R^i] - R_f = \beta_i (\mathbb{E}[R^{mkt}] - R_f)$.

**Alpha is the deviation from the SML.** Under the CAPM, $\alpha = 0$ for all assets. Persistent positive alphas imply either a violation of the model or a mispriced market proxy.

**The CAPM rests on strong assumptions, many of which are violated in practice.** Non-normality, heterogeneous beliefs, borrowing constraints, and non-tradable assets each generate deviations. The Roll critique shows that the true market portfolio is unobservable, making the CAPM difficult to definitively test or reject.

**Empirical evidence reveals systematic anomalies — size, value, momentum — that beta alone cannot explain.** These anomalies motivate multi-factor extensions, which we develop in Block 2.3 within the same SDF language.

---

## Looking Ahead: Block 2.3 — Factor Models and the APT

The CAPM is a single-factor model — the sole priced risk is exposure to aggregate market fluctuations. Block 2.3 generalizes this to multi-factor models. We develop the **Arbitrage Pricing Theory** (APT) of Ross (1976), which derives a multi-factor pricing equation from the assumption of approximate arbitrage-free pricing in a large economy — without any equilibrium argument. We then examine the **Fama-French** family of models as empirical implementations of the APT, and establish precisely what conditions a set of empirical factors must satisfy to constitute a valid SDF. The unifying theme remains the SDF: every additional factor is an additional dimension in which the pricing kernel varies, and the central question is always which risks the market actually compensates.

---

*Block 2.1 — The SDF Framework | **Block 2.2 — Mean-Variance Frontier and the CAPM** | Block 2.3 — Factor Models and the APT →*
