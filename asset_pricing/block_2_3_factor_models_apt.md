# Block 2.3 — Factor Models and the Arbitrage Pricing Theory

> *"The APT is not a theory about what the factors are. It is a theory about what expected returns must look like if there are no arbitrage opportunities in a large economy."*
> — Stephen Ross, *Journal of Economic Theory* (1976)

---

## Where We Left Off

Block 2.2 ended with a verdict: the CAPM contains important truth, but a single beta with respect to the market portfolio cannot explain the full cross-section of expected returns. Size, value, and momentum — among other characteristics — predict returns in ways that market beta alone does not. The natural response is to add factors. But this raises immediate and deep questions. Which factors should we include? Why should multiple factors be priced in equilibrium? What is the theoretical foundation for multi-factor pricing, and how do we know when we have found the right set of factors? How do we distinguish a genuine risk factor from a spurious pattern in historical data?

This block develops the answers systematically. We begin with the **Arbitrage Pricing Theory** (APT), which provides the most general theoretical foundation for multi-factor models — derived not from equilibrium but from the much weaker assumption of approximate absence of arbitrage. We then examine the major empirical factor models, interpret them through the SDF lens, and develop the tools needed to evaluate them rigorously. Throughout, the SDF framework of Block 2.1 provides the unifying language.

---

## 1. The Factor Structure of Returns

### The Exact Factor Model

The APT begins with an assumption about the **structure of returns**, not about preferences or equilibrium. Suppose the return on every asset $i$ can be written as:

$$
R^i = \mathbb{E}[R^i] + \sum_{k=1}^{K} \beta^i_k f_k + \varepsilon^i
$$

where $f_1, \ldots, f_K$ are **common factors** — random variables with zero mean that affect many assets simultaneously — $\beta^i_k$ are the **factor loadings** or **betas** of asset $i$ on factor $k$, and $\varepsilon^i$ is an **idiosyncratic shock** specific to asset $i$.

The key assumption is that the idiosyncratic shocks are mutually uncorrelated: $\text{Cov}(\varepsilon^i, \varepsilon^j) = 0$ for $i \neq j$, and uncorrelated with all factors: $\text{Cov}(\varepsilon^i, f_k) = 0$ for all $i, k$. All co-movement between assets is captured by their common factor loadings.

This structure has a compelling empirical motivation. The correlation matrix of a large cross-section of equity returns is far from diagonal — stocks move together far more than their individual characteristics would suggest. The factor model asserts that this co-movement is driven by a small number of pervasive forces: the business cycle, monetary policy shifts, changes in credit conditions, and so on. Idiosyncratic news — a firm-specific earnings surprise, a product recall — drives $\varepsilon^i$ but not $f_k$.

The covariance matrix implied by the exact factor model is:

$$
\boldsymbol{\Sigma} = \mathbf{B}\boldsymbol{\Sigma}_f\mathbf{B}' + \mathbf{D}
$$

where $\mathbf{B}$ is the $N \times K$ matrix of factor loadings, $\boldsymbol{\Sigma}_f$ is the $K \times K$ covariance matrix of factors, and $\mathbf{D}$ is the diagonal matrix of idiosyncratic variances. This decomposition is the basis of **principal component analysis** (PCA) applied to returns: the eigenvectors of $\boldsymbol{\Sigma}$ with the largest eigenvalues correspond to the dominant factors.

### The Approximate Factor Model

In practice, the exact orthogonality of idiosyncratic shocks is too strong — firms in the same industry share common shocks (say, an oil price change affects all energy companies) that are not captured by the market factor alone. The **approximate factor model** (Chamberlain and Rothschild, 1983) weakens the assumption: idiosyncratic covariances are allowed, but they must be small in a precise sense — the largest eigenvalue of the idiosyncratic covariance matrix must remain bounded as $N \to \infty$, while the eigenvalues associated with the common factors must diverge.

Intuitively, each common factor affects many assets, so its contribution to the covariance matrix grows with $N$. Idiosyncratic shocks affect only a few assets each, so their aggregate contribution to portfolio variance is bounded. This distinction — between pervasive factors and localized idiosyncratic shocks — is the empirical content of the APT.

---

## 2. The Arbitrage Pricing Theory

### The Core Argument

Now we derive the APT. The argument is remarkably elegant and requires almost nothing beyond the factor structure and the law of large numbers.

Consider a **well-diversified portfolio**: a portfolio of $N$ assets with weights $w_i = 1/N$ (or more generally, weights that shrink to zero as $N \to \infty$). The return on such a portfolio is:

$$
R^p = \mathbb{E}[R^p] + \sum_{k=1}^{K} \beta^p_k f_k + \varepsilon^p
$$

where $\beta^p_k = \sum_i w_i \beta^i_k$ are the portfolio's factor loadings and $\varepsilon^p = \sum_i w_i \varepsilon^i$ is the portfolio's idiosyncratic shock. By the law of large numbers (and the approximate orthogonality of idiosyncratic shocks):

$$
\text{Var}(\varepsilon^p) = \sum_i w_i^2 \text{Var}(\varepsilon^i) \leq \frac{1}{N} \max_i \text{Var}(\varepsilon^i) \to 0 \text{ as } N \to \infty
$$

In the limit, a well-diversified portfolio has **no idiosyncratic risk**. Its return is entirely determined by its factor exposures:

$$
R^p \approx \mathbb{E}[R^p] + \sum_{k=1}^{K} \beta^p_k f_k
$$

Now consider two well-diversified portfolios $A$ and $B$ with identical factor loadings: $\beta^A_k = \beta^B_k$ for all $k$. These portfolios have the same exposure to every systematic risk. In a large economy, they are therefore **essentially identical** random variables. If their expected returns differ — say $\mathbb{E}[R^A] > \mathbb{E}[R^B]$ — then the portfolio long $A$ and short $B$ is:

- Self-financing (zero cost, since we are long and short in equal amounts)
- Factor-neutral (identical loadings cancel)
- Approximately riskless (negligible idiosyncratic variance)
- Profitable in expectation ($\mathbb{E}[R^A - R^B] > 0$)

This is an **approximate arbitrage** — a free lunch in the limit. In an economy with many assets, investors would immediately exploit this opportunity, driving $\mathbb{E}[R^A]$ down and $\mathbb{E}[R^B]$ up until the difference disappears. The absence of approximate arbitrage therefore forces:

$$
\mathbb{E}[R^A] = \mathbb{E}[R^B] \quad \text{whenever } \beta^A_k = \beta^B_k \text{ for all } k
$$

Expected returns must be a function of factor loadings alone. The only linear function consistent with this and with the risk-free asset pricing at $R_f$ is:

$$
\boxed{\mathbb{E}[R^i] = R_f + \sum_{k=1}^{K} \beta^i_k \lambda_k}
$$

where $\lambda_k$ is the **factor risk premium** — the expected excess return on a portfolio with unit loading on factor $k$ and zero loading on all other factors. This is the APT pricing equation.

### What the APT Is — and Is Not

The APT is a statement about approximate arbitrage in large economies, not about equilibrium or preferences. This gives it both strength and limitation:

**Strength**: The APT holds for any agents who prefer more to less, regardless of the shape of their utility functions. It does not require normality of returns, quadratic utility, or any specific preference structure beyond monotonicity. It is considerably more general than the CAPM.

**Limitation**: The APT does not tell us what the factors are, how many there are, or what the factor risk premia $\lambda_k$ should be. These are empirical questions. The CAPM, by contrast, identifies a specific factor (the market portfolio) from equilibrium reasoning and gives the premium in terms of the market risk premium — a quantity with a clear economic interpretation. The APT's agnosticism about factors is simultaneously its greatest strength (flexibility) and its greatest weakness (empirical ambiguity).

**The exact versus approximate distinction**: The APT holds exactly only in the limit of infinitely many assets and only for well-diversified portfolios. For individual stocks, the idiosyncratic residual $\varepsilon^i$ remains, and exact pricing requires additional conditions (essentially, complete markets or specific preferences). This is in contrast to the CAPM, which holds exactly for every asset under its assumptions.

---

## 3. Factor Risk Premia: What Gets Compensated?

The APT tells us that factor risk premia $\lambda_k$ exist, but gives no guidance on their magnitudes or even signs. A factor deserves a positive premium if and only if it represents a **systematic risk that investors genuinely dislike** — a source of fluctuations in wealth that cannot be diversified away and that coincides with bad times.

This brings us back to the SDF. In the SDF framework, a factor $f_k$ is priced (has $\lambda_k \neq 0$) if and only if $\text{Cov}(f_k, m) \neq 0$ — if the factor covaries with the stochastic discount factor. A factor that is correlated with the SDF represents a genuine source of risk about which investors care; a factor that is orthogonal to $m$ carries no premium regardless of how much variance it contributes to returns.

This connects the empirical factor literature to the theoretical asset pricing framework. When researchers find that a new variable predicts the cross-section of returns, the economic question is: what is this variable a proxy for in the SDF? Size, for instance, predicts returns — but is the size premium a compensation for distress risk (small firms are more vulnerable to recessions), for illiquidity (small stocks are harder to trade), or for mispricing (small firms receive less analyst coverage and may be systematically misvalued)? The empirical fact of a size premium is not contested; its interpretation as a risk premium versus an anomaly is.

---

## 4. The Major Empirical Factor Models

### 4.1 The Fama-French Three-Factor Model (1993)

Fama and French (1993) proposed extending the CAPM with two additional factors motivated by the anomalies documented in their 1992 paper:

$$
R^i - R_f = \alpha^i + \beta^i_{mkt}(R^{mkt} - R_f) + \beta^i_{SMB} \cdot SMB + \beta^i_{HML} \cdot HML + \varepsilon^i
$$

where:

- **SMB** (Small Minus Big) is the return on a portfolio long small-cap stocks and short large-cap stocks, capturing the **size premium**.
- **HML** (High Minus Low) is the return on a portfolio long high book-to-market ("value") stocks and short low book-to-market ("growth") stocks, capturing the **value premium**.

The factors are constructed as self-financing portfolios — long one side, short the other — so they represent zero-cost investment strategies with expected returns equal to the factor premia $\lambda_{SMB}$ and $\lambda_{HML}$.

Empirically, the three-factor model absorbs most of the size and value anomalies that plagued the CAPM. The alphas of size-sorted and book-to-market-sorted portfolios are close to zero after controlling for SMB and HML exposures. The model achieves $R^2$ values of 90% or higher in time-series regressions for diversified portfolios — a dramatic improvement over the single-factor CAPM.

The economic interpretation of SMB and HML remains debated. Fama and French themselves initially leaned toward a risk-based explanation: small and value stocks are riskier in ways that the market beta does not capture — perhaps they are more exposed to financial distress or to cyclical fluctuations in the investment opportunity set. The alternative behavioral view holds that investors systematically overprice growth stocks and underprice value stocks due to extrapolation of past earnings growth, and that the value premium reflects a correction of this mispricing. After three decades of research, both explanations retain empirical support, and the debate has not been definitively resolved.

### 4.2 The Carhart Four-Factor Model (1997)

Jegadeesh and Titman (1993) documented that stocks with high returns over the past 6–12 months continue to outperform over the following 6–12 months — the **momentum effect**. Carhart (1997) incorporated this into a four-factor model by adding:

- **UMD** (Up Minus Down, or WML: Winners Minus Losers): the return on a portfolio long past winners and short past losers.

$$
R^i - R_f = \alpha^i + \beta^i_{mkt}(R^{mkt} - R_f) + \beta^i_{SMB} \cdot SMB + \beta^i_{HML} \cdot HML + \beta^i_{UMD} \cdot UMD + \varepsilon^i
$$

Momentum is perhaps the most puzzling anomaly for risk-based explanations. It operates at the 6–12 month horizon (shorter-term returns tend to reverse — the short-term reversal of Jegadeesh, 1990) and dissipates beyond 12–18 months (the long-term reversal of De Bondt and Thaler, 1985). The pattern is consistent with underreaction to information — investors update their beliefs too slowly in response to earnings surprises and other fundamental news. The risk-based alternative has struggled to provide a convincing account: what systematic risk is the momentum factor a proxy for that could justify the 1–1.5% monthly premium it earns?

Daniel and Moskowitz (2016) showed that momentum strategies are subject to dramatic "crashes" — large, sudden losses that tend to occur at market rebounds following periods of market stress. This crash risk provides a partial risk-based explanation: momentum is compensation for left-tail risk exposure concentrated in bad economic times, consistent with a high SDF price for crash states.

### 4.3 The Fama-French Five-Factor Model (2015)

Fama and French (2015) extended their three-factor model by adding two factors motivated by a dividend discount model decomposition of the book-to-market ratio:

- **RMW** (Robust Minus Weak): the return on a portfolio long firms with high operating profitability and short firms with low profitability.
- **CMA** (Conservative Minus Aggressive): the return on a portfolio long low-investment ("conservative") firms and short high-investment ("aggressive") firms.

$$
R^i - R_f = \alpha^i + \beta^i_{mkt}(R^{mkt} - R_f) + \beta^i_{SMB} \cdot SMB + \beta^i_{HML} \cdot HML + \beta^i_{RMW} \cdot RMW + \beta^i_{CMA} \cdot CMA + \varepsilon^i
$$

The theoretical motivation draws on the **q-theory of investment** (Hou, Xue, and Zhang, 2015) and the **dividend discount model**: in a standard valuation model, expected returns are higher for firms with lower prices relative to fundamentals (value), higher profitability, and lower investment (since high investment dilutes existing shareholders and signals low discount rates). The five-factor model provides a disciplined way of operationalizing these valuation relationships as return predictors.

The five-factor model largely absorbs the value premium (HML becomes redundant once profitability and investment are controlled for), but it famously does **not** subsume momentum — UMD remains a significant predictor of returns even after conditioning on the five factors. This suggests that momentum and value operate through distinct mechanisms.

### 4.4 The $q$-Factor Model (Hou, Xue, and Zhang, 2015)

Hou, Xue, and Zhang (2015) proposed an alternative four-factor model grounded in investment theory. Their factors are:

- **$R^{MKT}$**: the market excess return.
- **$R^{ME}$**: a size factor (small minus big by market equity).
- **$R^{IA}$**: an investment factor (low investment minus high investment, analogous to CMA).
- **$R^{ROE}$**: a profitability factor (high ROE minus low ROE, analogous to RMW).

The $q$-factor model is motivated by the first-order conditions of a firm's investment problem in a neoclassical framework. Expected stock returns equal the cost of equity capital, which in the model is determined by the firm's investment rate and return on equity. High-investment firms have low expected returns because they are expanding capital when marginal $q$ is low; high-profitability firms have high expected returns because their marginal product of capital is high.

This model has strong theoretical microfoundations compared to the empirically-motivated Fama-French approach. It performs comparably or better on many standard test portfolios, and its factors have clearer economic interpretations. Whether the theoretical grounding gives it a decisive advantage is still debated.

---

## 5. The Factor Zoo and the Multiple Testing Problem

By the early 2020s, the academic literature had proposed over **400 factors** purportedly able to predict the cross-section of returns. Cochrane (2011) famously called this the **"factor zoo"** — a proliferation of anomalies and factors with no coherent theoretical structure and serious concerns about spurious discovery.

### The Multiple Testing Problem

When researchers test hundreds of factors using the same dataset, the probability of finding spurious predictors by chance is high. If we test 400 factors at a 5% significance level, we expect 20 false positives even if none of the factors is genuinely priced — simply due to sampling variation. The standard $t$-statistic threshold of 2.0 (corresponding to 5% significance with one test) is therefore far too lenient when hundreds of tests have been conducted.

Harvey, Liu, and Zhu (2016) argued that the appropriate $t$-statistic threshold, accounting for multiple testing, should be at least 3.0 — corresponding to a significance level of roughly 0.3%. By this standard, many factors in the literature would not survive. McLean and Pontiff (2016) showed empirically that the returns to factor strategies decline sharply after their publication, consistent with the idea that many discovered factors reflect data mining rather than genuine risk premia.

### Addressing the Multiple Testing Problem

Several approaches have been proposed:

**Multiple testing corrections**: The Bonferroni correction, the Benjamini-Hochberg procedure, and related methods adjust the significance threshold to control the family-wise error rate or the false discovery rate. Harvey, Liu, and Zhu (2016) advocate for their use in all factor studies.

**Out-of-sample testing**: A factor that is robust should survive when tested on data not used in its discovery — either an international sample, a different time period, or an out-of-sample holdout period. Factors discovered in US data that fail to replicate internationally are suspect.

**Economic plausibility**: A factor should have a credible economic story. A factor that predicts returns in historical data but has no plausible connection to the SDF — no obvious interpretation as a systematic risk or a persistent mispricing mechanism — deserves greater skepticism.

**Machine learning approaches**: Gu, Kelly, and Xiu (2020) applied a battery of machine learning methods — LASSO, gradient boosting, neural networks — to predict returns using hundreds of firm characteristics simultaneously. These methods impose penalization that naturally selects among predictors, mitigating the multiple testing problem. Their findings suggest that nonlinear interactions among characteristics have significant predictive power beyond what linear factor models capture.

---

## 6. What Makes a Valid Factor? The SDF Perspective

From the SDF perspective, the proliferation of factors takes on a cleaner structure. Any set of excess return factors $f_1, \ldots, f_K$ spans a valid SDF if and only if the linear combination:

$$
m = a + b_1 f_1 + \cdots + b_K f_K
$$

satisfies $\mathbb{E}[mR^i] = 1$ for all test assets. This is an **exact** pricing condition — not just a statement that the factors predict the cross-section. Many empirical factor models satisfy this pricing condition *approximately* but not exactly, leaving nonzero alphas for some portfolios.

The SDF perspective also clarifies what "spanning" means. A new factor $f_{K+1}$ adds value to an existing model if and only if it lies outside the space already spanned by $f_1, \ldots, f_K$ — equivalently, if it has a nonzero weight in the minimum-variance SDF that is orthogonal to the existing factors. If $f_{K+1}$ is a linear combination of existing factors, it adds nothing to the pricing kernel even if it is individually significant in cross-sectional regressions.

This motivates a practical criterion: a new factor is genuine if adding it to the SDF significantly reduces the **Hansen-Jagannathan distance** for the relevant set of test portfolios. Factors that reduce HJ distance are adding genuine pricing power; factors that improve $R^2$ in cross-sectional regressions without reducing HJ distance may be capturing noise.

---

## 7. The Two Empirical Methodologies: Time-Series vs. Cross-Sectional Regressions

Factor models can be estimated in two complementary ways, each testing a slightly different hypothesis.

### Time-Series (First-Pass) Regression

Regress each asset's excess return on the factors over time:

$$
R^i_t - R_{f,t} = \alpha^i + \sum_{k=1}^{K} \beta^i_k f_{k,t} + \varepsilon^i_t
$$

The factor loadings $\beta^i_k$ are estimated. The APT predicts that $\alpha^i = 0$ for all assets — no asset should earn excess returns beyond what its factor exposures justify. A **GRS test** (Gibbons, Ross, and Shanken, 1989) jointly tests $H_0: \alpha^i = 0$ for all $i$, accounting for the correlation structure of the residuals. Rejection of this null means the factors fail to price at least some assets.

The time-series approach is natural when factors are traded portfolios (excess returns), because the factor premia $\lambda_k$ are directly estimated as the time-series average of $f_{k,t}$. The market excess return, SMB, HML, and similar factors are all traded — their average returns over the sample are the estimated premia.

### Cross-Sectional (Second-Pass, Fama-MacBeth) Regression

Given estimated betas from the time-series regressions, run a cross-sectional regression of average returns on betas:

$$
\bar{R}^i - \bar{R}_f = \lambda_0 + \sum_{k=1}^{K} \beta^i_k \hat{\lambda}_k + \eta^i
$$

The slope coefficients $\hat{\lambda}_k$ are the estimated factor risk premia. The intercept $\lambda_0$ should equal zero (or $R_f$ if using raw rather than excess returns). A positive and significant $\hat{\lambda}_k$ indicates that factor $k$ is priced in the cross-section — assets with higher loadings on that factor earn systematically higher returns.

The **Fama-MacBeth (1973)** procedure runs this cross-sectional regression month by month, using the time-series of cross-sectional slope estimates to compute standard errors that account for cross-sectional correlation. This procedure remains the standard approach in empirical asset pricing.

An important subtlety: when factors are not traded portfolios (e.g., macroeconomic variables like GDP growth or inflation), the factor premia must be estimated from the cross-sectional regression rather than read off from the factor's average return. This introduces additional estimation error and makes identification more demanding.

---

## 8. Connecting Everything: The SDF View of Factor Models

Let us close by placing the entire factor model literature within the SDF framework — making the connections explicit and precise.

A $K$-factor model with traded factors $f_1, \ldots, f_K$ implies an SDF of the form:

$$
m_t = 1 - \sum_{k=1}^{K} b_k (f_{k,t} - \mathbb{E}[f_k])
$$

where the $b_k$ are determined by the requirement that $\mathbb{E}[m_t R^i_t] = 1$ for all test assets. In matrix notation:

$$
\mathbf{b} = \boldsymbol{\Sigma}_f^{-1} \boldsymbol{\lambda}
$$

where $\boldsymbol{\Sigma}_f$ is the covariance matrix of factors and $\boldsymbol{\lambda}$ is the vector of factor premia. This is the **SDF representation** of the beta pricing model — the translation between the factor model's language (betas and premia) and the SDF language (loadings and the pricing kernel).

The hierarchical picture is now complete:

**No-arbitrage** $\Rightarrow$ **Existence of a positive SDF** $\Rightarrow$ **$p = \mathbb{E}[mx]$ for all assets**

$\Downarrow$

**Frontier-SDF duality** $\Rightarrow$ **Mean-variance efficiency** $\Leftrightarrow$ **Single-factor pricing (CAPM)**

$\Downarrow$

**Factor structure of returns + approximate no-arbitrage** $\Rightarrow$ **Multi-factor pricing (APT)** $\Rightarrow$ **$\mathbb{E}[R^i] = R_f + \sum_k \beta^i_k \lambda_k$**

$\Downarrow$

**Empirical implementation** $\Rightarrow$ **Fama-French, $q$-factor, Carhart, ...** (specific parametrizations of the SDF)

Every step in this hierarchy is a restriction — either on the SDF directly, or on the structure of returns and the pricing it implies. Testing a factor model is testing whether a specific parametrization of $m$ is consistent with observed prices. When the model fails — when alphas are nonzero, when the HJ distance is large, when the GRS test rejects — it tells us that the true SDF requires dimensions that the proposed factors do not capture.

The task of empirical asset pricing is to identify those dimensions. The factor zoo, for all its excess, represents a collective attempt by the profession to map out the shape of the pricing kernel — to discover which systematic risks the market actually compensates, and at what price.

---

## Key Takeaways

**The factor structure of returns asserts that all co-movement among assets is driven by a small number of pervasive common factors.** Idiosyncratic shocks diversify away in large portfolios; systematic factor risk does not.

**The APT derives multi-factor pricing from approximate no-arbitrage alone.** No equilibrium, no specific preferences, no normality required — only the absence of approximate arbitrage in large economies. Expected returns are linear in factor loadings: $\mathbb{E}[R^i] = R_f + \sum_k \beta^i_k \lambda_k$.

**Factor risk premia are determined by covariance with the SDF.** A factor is priced if and only if it is correlated with the pricing kernel. The economic question behind every anomaly is: what is this variable measuring about the SDF?

**The major empirical models — Fama-French three-factor, Carhart four-factor, Fama-French five-factor, $q$-factor — are specific parametrizations of the SDF.** They differ in which factors they include, how those factors are constructed, and what economic mechanism they invoke to explain premia.

**The factor zoo and the multiple testing problem demand methodological rigor.** With hundreds of proposed factors, the probability of spurious discovery is high. Valid factors must survive out-of-sample tests, exhibit economic plausibility, and demonstrably reduce the HJ distance for relevant test assets.

**Time-series and cross-sectional regressions are complementary tools.** The GRS test checks whether alphas are jointly zero (time-series); Fama-MacBeth regressions estimate factor premia from the cross-section. Together, they constitute the empirical toolkit for factor model evaluation.

---

## Looking Ahead: Block 3.1 — The Equity Premium Puzzle and Its Discontents

Part 2 has built the complete SDF-based architecture of modern asset pricing. We now shift from *structure* to *quantification*. The equity premium puzzle — first encountered at the end of Block 1.3 and re-derived through the Hansen-Jagannathan bound in Block 2.1 — is the central quantitative challenge for consumption-based models. Block 3.1 examines the puzzle in full depth: its original derivation by Mehra and Prescott (1985), the joint puzzle with the risk-free rate (Weil, 1989), the calibration strategy and its assumptions, and the landscape of proposed resolutions. This block marks the transition from the foundational framework to the frontier of the field — where the models are more elaborate, the assumptions more contested, and the economic insights more hard-won.

---

*Block 2.2 — Mean-Variance Frontier and the CAPM | **Block 2.3 — Factor Models and the APT** | Block 3.1 — The Equity Premium Puzzle →*
