# Block 2.1 — The Stochastic Discount Factor: A Universal Pricing Language

> *"All of asset pricing can be viewed as an attempt to understand the stochastic discount factor."*
> — John Cochrane, *Asset Pricing* (2005)

---

## Where We Left Off

Block 1.3 ended with a remarkable equation. Starting from nothing more than an agent who maximizes expected discounted utility, we derived:

$$
p_{i,t} = \mathbb{E}_t\!\left[ m_{t+1} \, x_{i,t+1} \right]
$$

where $x_{i,t+1}$ is the payoff of asset $i$ at time $t+1$, $p_{i,t}$ is its price today, and $m_{t+1} = \beta \, u'(c_{t+1})/u'(c_t)$ is the **stochastic discount factor** — a random variable that inherits its randomness from the uncertainty in future consumption.

This block begins a pivotal shift in perspective. Rather than asking "what specific utility function generates $m$?", we ask: **what must be true of any valid $m$, regardless of where it comes from?** It turns out that the equation $p = \mathbb{E}[mx]$ is not just the result of one particular model — it is a near-universal statement about prices in any economy that is even approximately free of arbitrage. Every serious model in asset pricing — the CAPM, the APT, the consumption-CAPM, option pricing models, term structure models — is a specific theory of what $m$ looks like. The SDF framework is the language in which all of these models can be written, compared, and tested.

We develop this language carefully, building from the absence of arbitrage up through the geometry of mean-variance frontiers and the Hansen-Jagannathan bound.

---

## 1. The Payoff Space and Prices

Begin with a clean setup. There are two dates: $t = 0$ (today) and $t = 1$ (tomorrow). At $t=1$, one of $S$ possible states of the world is realized, with probabilities $\pi_1, \ldots, \pi_S > 0$. An **asset** is defined by its payoff vector $x = (x_1, \ldots, x_S) \in \mathbb{R}^S$, where $x_s$ is the payoff in state $s$. The price of asset $x$ at $t=0$ is $p(x) \in \mathbb{R}$.

Let $\mathcal{X}$ denote the **payoff space** — the set of all payoff vectors that can be achieved by trading available assets and their portfolios. If there are $N$ basis assets with payoff vectors $x^1, \ldots, x^N$ and prices $p^1, \ldots, p^N$, then $\mathcal{X} = \text{span}\{x^1, \ldots, x^N\}$, and the pricing function extends linearly: a portfolio $\theta = (\theta_1, \ldots, \theta_N)$ has payoff $\sum_i \theta_i x^i$ and price $\sum_i \theta_i p^i$.

We make one key assumption on the pricing function: **linearity**. The price of a portfolio equals the sum of the prices of its components. No transaction costs, no short-sale constraints that affect prices, no market power. This is the standard frictionless market assumption, and it ensures that $p: \mathcal{X} \to \mathbb{R}$ is a linear functional.

---

## 2. The Law of One Price and the Absence of Arbitrage

Two conditions of increasing strength restrict what prices can look like.

### The Law of One Price (LOOP)

The **law of one price** states that portfolios with identical payoffs must have identical prices:

$$
x = y \implies p(x) = p(y)
$$

This is the minimal requirement for a price system to be coherent. If two portfolios always deliver the same payoff in every state of the world, yet trade at different prices, any investor would immediately sell the expensive one and buy the cheap one, forcing prices to converge. The LOOP is therefore an equilibrium condition, not an assumption about preferences.

The LOOP is equivalent to linearity of the pricing function on $\mathcal{X}$ — which we have already assumed. It has a powerful representation:

**Theorem (Riesz Representation)**: If the law of one price holds, there exists a random variable $m^* \in \mathcal{X}$ such that for all $x \in \mathcal{X}$:

$$
p(x) = \mathbb{E}[m^* x]
$$

The random variable $m^*$ is the **minimum-variance SDF** — the unique element of $\mathcal{X}$ that prices all assets correctly. This is a purely algebraic result; it follows from the fact that any linear functional on a Hilbert space can be represented as an inner product with a unique element of that space. Think of $\mathbb{E}[xy]$ as the inner product: the pricing functional $p(x)$ can then be "represented" by $m^*$ via this inner product.

### No-Arbitrage

The **absence of arbitrage** (NA) is a stronger condition. An **arbitrage portfolio** is one that:
- Has a non-positive price: $p(x) \leq 0$, and
- Has a non-negative payoff in every state: $x_s \geq 0$ for all $s$, with $x_s > 0$ for at least one state.

Put simply, an arbitrage is something for nothing — a costless bet with no downside. Competitive markets quickly eliminate arbitrage opportunities as traders exploit them.

**Theorem (Fundamental Theorem of Asset Pricing, FTAP)**: The following are equivalent:
1. There is no arbitrage.
2. There exists a **strictly positive** random variable $m > 0$ (in all states) such that $p(x) = \mathbb{E}[mx]$ for all $x \in \mathcal{X}$.
3. There exists a **risk-neutral probability measure** $\mathbb{Q}$ (with $\mathbb{Q}(s) > 0$ for all $s$) such that $p(x) = R_f^{-1} \mathbb{E}^{\mathbb{Q}}[x]$ for all $x \in \mathcal{X}$.

Conditions 2 and 3 are equivalent via $m = \mathbb{Q}(s) / (\pi_s R_f)$ — the SDF is the ratio of risk-neutral to physical probabilities, deflated by the risk-free rate. The strict positivity of $m$ is the key addition beyond LOOP: it ensures that states with positive probability get positive pricing weight, ruling out arbitrage.

The FTAP is the bedrock of modern financial economics. It tells us that price systems immune to arbitrage can *always* be written as $p(x) = \mathbb{E}[mx]$ for some strictly positive $m$, and conversely. The specific choice of $m$ — which depends on preferences, endowments, and beliefs — is what distinguishes one model from another.

---

## 3. The Multiplicity of SDFs

A critical subtlety: the SDF is **not unique** unless markets are complete.

**Complete markets**: A market is complete if every possible payoff vector in $\mathbb{R}^S$ can be replicated by trading available assets — equivalently, if $\mathcal{X} = \mathbb{R}^S$. In complete markets, the SDF is unique: there is only one strictly positive random variable that prices every possible payoff correctly.

**Incomplete markets**: When $\mathcal{X}$ is a proper subspace of $\mathbb{R}^S$ (fewer independent assets than states), the SDF is not uniquely pinned down by $p(x) = \mathbb{E}[mx]$ for $x \in \mathcal{X}$. Any $m$ can be decomposed as:

$$
m = m^* + \varepsilon
$$

where $m^* \in \mathcal{X}$ is the unique **minimum-variance SDF** (the projection of $m$ onto $\mathcal{X}$), and $\varepsilon$ is an element orthogonal to $\mathcal{X}$ in the sense that $\mathbb{E}[\varepsilon x] = 0$ for all $x \in \mathcal{X}$. The residual $\varepsilon$ is uncorrelated with all traded payoffs and hence has no effect on prices — but it affects the variance of $m$.

This decomposition is crucial for testing. When we estimate or test an SDF — say, one derived from a consumption-based model — we can decompose the model's proposed $m$ into the part that matters for pricing ($m^*$, which must be the same for all valid models) and the residual ($\varepsilon$, which is model-specific and untestable from prices alone). What is testable is whether a proposed $m$ has the right $m^*$ component — equivalently, whether the model correctly captures the priced sources of risk.

---

## 4. From the SDF to Expected Returns

Rewrite the fundamental pricing equation in terms of returns. For an asset with price $p > 0$, define its gross return $R = x/p$. Then $p = \mathbb{E}[mx]$ becomes:

$$
1 = \mathbb{E}[mR]
$$

This single equation has rich implications. First, apply it to the risk-free asset (which pays $R_f$ in every state, so $R_f = 1/\mathbb{E}[m]$):

$$
1 = \mathbb{E}[m] \cdot R_f \quad \Longrightarrow \quad R_f = \frac{1}{\mathbb{E}[m]}
$$

Now use the covariance decomposition $\mathbb{E}[mR] = \mathbb{E}[m]\mathbb{E}[R] + \text{Cov}(m, R)$:

$$
1 = \mathbb{E}[m]\mathbb{E}[R] + \text{Cov}(m, R)
$$

Substituting $\mathbb{E}[m] = 1/R_f$:

$$
\mathbb{E}[R] - R_f = -R_f \cdot \text{Cov}(m, R)
$$

This is the **fundamental expected return equation**. The expected excess return on any asset equals $-R_f$ times the covariance of its return with the SDF. Let us read this carefully:

- **Assets that covary negatively with $m$ have positive expected excess returns.** Since $m = \beta u'(c_{t+1})/u'(c_t)$, high $m$ occurs when consumption is low and marginal utility is high — bad economic times. An asset that pays poorly in bad times (negative covariance with $m$) is unattractive; investors demand a premium to hold it.
- **Assets that covary positively with $m$ have negative expected excess returns** — they are "insurance" assets that pay off precisely when investors need it most. Investors willingly accept lower returns to hold them.
- **The risk-free rate** does not depend on covariance — it is determined solely by $\mathbb{E}[m]$, reflecting time preference and precautionary savings.

This is the deepest result in all of asset pricing, stated with complete generality: **risk is not variance; it is covariance with the SDF**. Variance that is uncorrelated with $m$ earns no premium — it is diversifiable. Only exposure to the "systematic risk" captured by $m$ is compensated.

---

## 5. Beta Representations and Factor Models

The expected return equation can be rewritten in a familiar beta form. Divide both sides by $\text{Var}(m)/\mathbb{E}[m]$:

$$
\mathbb{E}[R^i] - R_f = \beta^i_m \cdot \lambda_m
$$

where:

$$
\beta^i_m = \frac{\text{Cov}(R^i, m)}{\text{Var}(m)}, \qquad \lambda_m = -R_f \cdot \frac{\text{Var}(m)}{\mathbb{E}[m]/R_f} \cdot \frac{\mathbb{E}[m]}{1}= -\frac{\text{Cov}(R^i, m)}{\text{Var}(m)} \cdot R_f \cdot \text{Var}(m) / \beta^i_m
$$

More cleanly, using the regression of $m$ on returns: any valid SDF can be written as $m = a + b \cdot f$ for some factor $f$ (or vector of factors), and expected returns satisfy:

$$
\mathbb{E}[R^i] - R_f = \beta^i_f \cdot \lambda_f
$$

where $\beta^i_f$ is the regression coefficient of $R^i$ on $f$, and $\lambda_f$ is the **factor risk premium** — the compensation per unit of factor exposure. This is the **beta pricing model** or **factor model** representation. The CAPM, for instance, is the special case where $f = R^m$ (the market return), which is valid when $m$ is linear in $R^m$ — as it is when all investors have mean-variance preferences or when returns are elliptically distributed.

The critical insight is that beta pricing models are not independent theories — they are all restrictions on the SDF. A factor model with factors $f_1, \ldots, f_K$ is the claim that $m = a + b_1 f_1 + \cdots + b_K f_K$ for some constants $a, b_1, \ldots, b_K$. Testing whether the CAPM or the Fama-French model "works" is equivalent to testing whether a specific linear combination of observed factors is a valid SDF.

---

## 6. The Hansen-Jagannathan Bound

We now derive one of the most important and elegant results in the empirical asset pricing literature — the **Hansen-Jagannathan (HJ) bound** (1991). It provides a model-free lower bound on the volatility of any valid SDF, derived purely from observable asset prices.

### Derivation

For any asset $i$, the expected return equation gives:

$$
\mathbb{E}[R^i] - R_f = -R_f \cdot \text{Cov}(m, R^i) = -R_f \cdot \sigma_m \sigma_{R^i} \rho_{m, R^i}
$$

Since the correlation $\rho_{m, R^i} \in [-1, 1]$, we have:

$$
|\mathbb{E}[R^i] - R_f| \leq R_f \cdot \sigma_m \cdot \sigma_{R^i}
$$

Dividing by $\sigma_{R^i}$:

$$
\frac{|\mathbb{E}[R^i] - R_f|}{\sigma_{R^i}} \leq R_f \cdot \sigma_m
$$

The left-hand side is the **Sharpe ratio** of asset $i$. Dividing by $\mathbb{E}[m] = 1/R_f$:

$$
\boxed{\frac{\sigma(m)}{\mathbb{E}[m]} \geq \max_i \left| \frac{\mathbb{E}[R^i] - R_f}{\sigma_{R^i}} \right|}
$$

This is the **Hansen-Jagannathan bound**: the coefficient of variation of the SDF must be at least as large as the maximum Sharpe ratio achievable from any portfolio of traded assets. It is a volatility lower bound — any proposed $m$ with insufficient volatility cannot simultaneously price all assets correctly.

### Why It Matters

The HJ bound connects the abstract SDF machinery to directly observable quantities. The maximum Sharpe ratio is determined by the mean-variance frontier of traded assets — something we can estimate from return data. The SDF volatility is a property of the pricing kernel implied by a particular model. If a model's SDF is too smooth, it fails the bound and can be immediately rejected without even running a regression.

The bound delivered a devastating early verdict on the basic consumption-CAPM. US equity data suggests a maximum Sharpe ratio of roughly $0.5$ per annum. The bound therefore requires:

$$
\frac{\sigma(m)}{\mathbb{E}[m]} \geq 0.5
$$

Under CRRA utility, $m = \beta(c_{t+1}/c_t)^{-\gamma}$, so approximately $\sigma(m)/\mathbb{E}[m] \approx \gamma \sigma_c$ where $\sigma_c \approx 0.01$. To satisfy the bound:

$$
\gamma \cdot 0.01 \geq 0.5 \quad \Longrightarrow \quad \gamma \geq 50
$$

The same back-of-the-envelope from Block 1.3 — but now derived from a completely model-free bound rather than from any particular return. The equity premium puzzle is not an artifact of the specific preference specification; it is a consequence of the low volatility of consumption growth relative to equity returns, and it constrains *any* consumption-based model.

### The HJ Distance

The HJ framework can be extended into a specification test. For a proposed SDF $m(\theta)$ that may not exactly price all assets, define the **HJ distance**:

$$
\delta_{HJ} = \min_{\theta} \sqrt{\left(\mathbb{E}[mx] - p\right)' W \left(\mathbb{E}[mx] - p\right)}
$$

for some weighting matrix $W$. This gives a scalar measure of how far the proposed SDF is from the set of valid SDFs — a useful diagnostic when comparing competing models, since the model with the smallest HJ distance is closest to satisfying exact pricing. We will return to this when discussing empirical methods in Block 6.

---

## 7. The SDF and Risk-Neutral Pricing

The FTAP established that no-arbitrage is equivalent to the existence of a strictly positive SDF. It also established the existence of a risk-neutral measure $\mathbb{Q}$. Let us make the connection explicit and precise, as it will be essential when we move to derivative pricing in Block 5.

Define the **risk-neutral probability** of state $s$ as:

$$
q_s = \frac{m_s \pi_s}{\mathbb{E}[m]} = R_f \cdot m_s \pi_s
$$

Since $m_s > 0$ and $\pi_s > 0$, we have $q_s > 0$. And $\sum_s q_s = R_f \sum_s m_s \pi_s = R_f \mathbb{E}[m] = 1$. So $q$ is indeed a probability measure.

Under $\mathbb{Q}$, the pricing equation becomes:

$$
p(x) = \mathbb{E}[mx] = \frac{1}{R_f} \sum_s q_s x_s = \frac{1}{R_f} \mathbb{E}^{\mathbb{Q}}[x]
$$

Every asset is priced as if investors were **risk-neutral** — but under the *distorted* probability measure $\mathbb{Q}$ rather than the physical measure $\mathbb{P}$. The distortion $q_s/\pi_s = R_f m_s$ is called the **Radon-Nikodym derivative** or the **pricing kernel** from $\mathbb{P}$ to $\mathbb{Q}$. States that are scarce (receive high marginal utility, high $m_s$) receive inflated probability weight under $\mathbb{Q}$, relative to their physical likelihood $\pi_s$.

This is the foundation of **risk-neutral pricing** as used throughout derivatives markets. The Black-Scholes formula, for instance, prices options as discounted expected payoffs under $\mathbb{Q}$, where stock prices grow at the risk-free rate rather than their physical expected return. The risk-neutral measure absorbs all risk adjustments into the probability weights, keeping the discounting simple and model-free. Behind every $\mathbb{Q}$ is an SDF; behind every SDF is a risk-neutral measure. They are two languages for the same object.

---

## 8. Complete and Incomplete Markets — A Deeper Look

We noted earlier that the SDF is unique if and only if markets are complete. Let us develop this more carefully, as it has profound implications for asset pricing and welfare.

### Arrow-Debreu Securities

The most transparent way to think about complete markets is through **Arrow-Debreu securities** — primitive assets that pay $1$ in exactly one state and $0$ in all others. Denote the price of the Arrow-Debreu security for state $s$ as $q_s^{AD}$ (its "state price"). If all Arrow-Debreu securities are traded, markets are complete: any payoff vector $x \in \mathbb{R}^S$ can be replicated by holding $x_s$ units of the Arrow-Debreu security for each state $s$.

The SDF in complete markets is then:

$$
m_s = \frac{q_s^{AD}}{\pi_s}
$$

— the state price per unit of probability. This is the unique strictly positive SDF (given strictly positive state prices). Every agent in the economy, regardless of preferences, evaluates payoffs using this same $m$ in equilibrium: the competitive equilibrium in complete markets uniquely determines the pricing kernel.

In incomplete markets, state prices are not all revealed by traded assets. Different agents may hold different beliefs or preferences and yet all be consistent with observed prices — the SDF is only pinned down on the subspace spanned by traded payoffs. This has practical consequences: in incomplete markets, welfare analysis is harder, individual consumption insurance is limited, and asset pricing models must be more carefully specified about which risks are priced and which are not.

### The Hansen-Jagannathan Volatility Bound Revisited

Recall that the minimum-variance SDF $m^*$ is the projection of any valid $m$ onto $\mathcal{X}$. It satisfies:

$$
\text{Var}(m) = \text{Var}(m^*) + \text{Var}(\varepsilon) \geq \text{Var}(m^*)
$$

The HJ bound is in fact the statement that $\sigma(m^*)/\mathbb{E}[m]$ equals the maximum Sharpe ratio. Any valid SDF has at least this much volatility — and the minimum is achieved by $m^*$ itself, the SDF in the payoff space. Models that imply an SDF with too little volatility are asserting, implicitly, that the residual $\varepsilon$ has *negative* variance — a mathematical impossibility.

---

## 9. A Roadmap Through the SDF Zoo

The power of the SDF framework is that every major asset pricing model can be written as a specific theory of $m$. Having built the framework, it is worth pausing to sketch how the major models fit into it:

**The CAPM** (Sharpe, 1964; Lintner, 1965): $m = a - b \cdot R^{mkt}$. Expected returns are linear in market beta. Valid when returns are jointly normal or agents have quadratic utility. The factor is the market return.

**The Consumption-CAPM** (Breeden, 1979; Lucas, 1978): $m = \beta (c_{t+1}/c_t)^{-\gamma}$. The factor is aggregate consumption growth. Theoretically elegant, empirically challenged by the equity premium puzzle.

**The APT** (Ross, 1976): $m = a + b_1 f_1 + \cdots + b_K f_K$ where the $f_k$ are pervasive risk factors. Expected returns are linear in multiple betas. The factors are empirically determined rather than theory-prescribed.

**The Fama-French models**: Special cases of the APT where specific return-based factors (size, value, profitability, investment) span the SDF. Empirically motivated.

**Habit formation models** (Campbell and Cochrane, 1999): $m = \beta (u'(c_{t+1} - h_{t+1})/u'(c_t - h_t))$ where $h_t$ is a habit stock. The SDF is more volatile than in standard CRRA because marginal utility is evaluated relative to habit, amplifying the response to consumption fluctuations.

**Recursive preferences** (Epstein and Zin, 1989): The SDF separates the elasticity of intertemporal substitution from risk aversion, allowing high risk aversion without forcing implausibly low EIS. The SDF depends on both consumption growth and the return on aggregate wealth.

**Rare disaster models** (Barro, 2006): The SDF occasionally takes on extreme values when disaster states are realized. Even if disasters are rare, their contribution to $\mathbb{E}[mR]$ can be large, generating large risk premia.

Each of these is an attempt to build a more volatile, more realistic SDF that can satisfy the Hansen-Jagannathan bound at plausible parameter values. We will study several of them in depth in Parts 3 and 4 of the course.

---

## Key Takeaways

**The law of one price implies the existence of an SDF; no-arbitrage implies it is strictly positive.** These are the two pillars of the FTAP. Any pricing kernel that is strictly positive and satisfies $p(x) = \mathbb{E}[mx]$ for all traded payoffs is a valid SDF.

**The SDF is generally not unique.** In incomplete markets, any valid SDF can be decomposed into $m^* + \varepsilon$, where $m^* \in \mathcal{X}$ is the unique minimum-variance SDF and $\varepsilon$ is orthogonal to all traded payoffs. Models are tested by their $m^*$ component.

**Risk is covariance with the SDF.** The expected excess return on any asset is $-R_f \cdot \text{Cov}(m, R)$. Variance uncorrelated with $m$ earns no premium. This is the deepest result in asset pricing.

**Factor models are restrictions on the SDF.** Every beta pricing model — CAPM, APT, Fama-French — is the claim that $m$ is linear in a specific set of factors. The SDF framework unifies them.

**The Hansen-Jagannathan bound is a model-free volatility lower bound.** The coefficient of variation of any valid SDF must exceed the maximum Sharpe ratio of traded portfolios. This bound immediately exposes the weakness of the standard consumption-CAPM.

**The SDF and the risk-neutral measure are two faces of the same object.** $m_s = q_s/(\pi_s R_f)$. Risk-neutral pricing — the language of derivatives — is SDF pricing in disguise.

---

## Looking Ahead: Block 2.2 — Mean-Variance Frontier and the CAPM

Having established the SDF as the universal pricing language, we now specialize to the most famous special case: the Capital Asset Pricing Model. Block 2.2 will show that the mean-variance frontier of risky assets and the SDF are intimately related — in fact, every mean-variance efficient portfolio is an SDF, and every SDF corresponds to a mean-variance efficient portfolio. This equivalence will let us derive the CAPM with full rigor, understand exactly when and why it holds, and identify the conditions under which it fails — setting the stage for the multi-factor models in Block 2.3.

---

*Block 1.3 — Intertemporal Choice | **Block 2.1 — The SDF Framework** | Block 2.2 — Mean-Variance Frontier and the CAPM →*
