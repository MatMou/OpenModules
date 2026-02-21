# Block 1.2 — Risk Aversion: How Much Does Uncertainty Cost?

> *"The desire for certainty is one of the most persistent and consequential facts about human psychology — and about asset prices."*

---

## Where We Left Off

In Block 1.1, we established that a rational agent who satisfies the VNM axioms can be represented by an expected utility function. That is, she ranks lotteries by:

$$
U(L) = \sum_{s} \pi_s \, u(c_s)
$$

where $u(\cdot)$ is her **Bernoulli utility function** — a real-valued function over outcomes — and the $\pi_s$ are the objective probabilities of each state $s$.

This was a representation theorem. It told us *that* such a function exists, but it said nothing about what shape $u$ takes. That question — the shape of $u$ and what it implies — is the subject of this block.

The central insight we will develop is this: **the curvature of $u$ is risk aversion**. Not a consequence of risk aversion, not a proxy for it — the curvature itself *is* the concept, once we unpack what risk aversion means.

---

## 1. What Does It Mean to Be Risk Averse?

Start with the simplest possible setting. An agent faces a fair gamble: she receives $+\epsilon$ or $-\epsilon$ with equal probability, so the expected payoff is zero. A **risk-neutral** agent is indifferent between taking the gamble and receiving nothing. A **risk-averse** agent strictly prefers receiving nothing — she would pay something to avoid the gamble.

More generally, consider a lottery $\tilde{c}$ with expected value $\mathbb{E}[\tilde{c}] = \mu$. Define the agent's **certainty equivalent** $CE$ as the sure amount she finds equally attractive:

$$
u(CE) = \mathbb{E}[u(\tilde{c})]
$$

**Risk aversion** is then the statement that $CE < \mu$ — the agent accepts a sure amount *below* the expected payoff in order to avoid the uncertainty.

This is equivalent, by Jensen's inequality, to $u$ being **strictly concave**:

$$
u(\mathbb{E}[\tilde{c}]) > \mathbb{E}[u(\tilde{c})] \quad \Longleftrightarrow \quad u \text{ is strictly concave}
$$

So the agent who demands a sure €80,000 over a 50/50 lottery between €30,000 and €150,000 (expected value €90,000) is revealed to have a concave $u$. The gap $\mu - CE = €10,000$ is her **risk premium** — what she would pay for insurance, or equivalently, what must be added to a risky asset's expected return to make it attractive.

This is not a minor technical detail. The risk premium is the engine behind asset pricing: every equity premium, every credit spread, every option price is ultimately a monetization of this gap between $\mu$ and $CE$.

---

## 2. Measuring Risk Aversion: The Arrow-Pratt Coefficients

The certainty equivalent gives us a qualitative notion of risk aversion, but we need something quantitative — a number that tells us how risk averse an agent is and allows comparisons across agents and across wealth levels.

Consider a small fair gamble $\tilde{\epsilon}$ with $\mathbb{E}[\tilde{\epsilon}] = 0$ and $\text{Var}(\tilde{\epsilon}) = \sigma^2$. The risk premium $\pi$ satisfies:

$$
u(w - \pi) = \mathbb{E}[u(w + \tilde{\epsilon})]
$$

Expand both sides with a Taylor approximation around $w$. The right-hand side gives:

$$
\mathbb{E}[u(w + \tilde{\epsilon})] \approx u(w) + u'(w)\mathbb{E}[\tilde{\epsilon}] + \frac{1}{2}u''(w)\mathbb{E}[\tilde{\epsilon}^2] = u(w) + \frac{1}{2}u''(w)\sigma^2
$$

The left-hand side gives:

$$
u(w - \pi) \approx u(w) - u'(w)\pi
$$

Setting these equal:

$$
\pi \approx -\frac{u''(w)}{2u'(w)} \cdot \sigma^2 = \frac{1}{2} A(w) \cdot \sigma^2
$$

where we define the **Arrow-Pratt coefficient of absolute risk aversion**:

$$
\boxed{A(w) = -\frac{u''(w)}{u'(w)}}
$$

This is a local measure. At any wealth level $w$, $A(w)$ tells you how much the agent charges (per unit of variance) to bear a small fair gamble. The ratio $-u''/u'$ is natural: $u''$ captures the curvature (how fast marginal utility is falling) and dividing by $u'$ makes the measure invariant to affine transformations of $u$ — recall that expected utility is only defined up to positive affine transformations.

### Relative Risk Aversion

Sometimes we care about gambles that are proportional to wealth — a 10% gain or loss rather than a fixed €1,000. The natural measure is then the **coefficient of relative risk aversion**:

$$
\boxed{R(w) = -\frac{u''(w) \cdot w}{u'(w)} = A(w) \cdot w}
$$

$R(w)$ answers: if the agent faces a small gamble of $\pm \epsilon \cdot w$ (proportional to wealth), what fraction of expected wealth would she give up to avoid it? This is the measure that matters for most of asset pricing, since returns — not dollar changes — are what investors compare across assets.

---

## 3. Common Utility Functions and Their Properties

The beauty of the Arrow-Pratt framework is that it organizes the zoo of utility functions by their risk aversion properties. Let's examine the most important families.

### 3.1 Constant Absolute Risk Aversion (CARA): The Exponential

$$
u(c) = -\frac{1}{\alpha} e^{-\alpha c}, \quad \alpha > 0
$$

Computing: $u'(c) = e^{-\alpha c}$ and $u''(c) = -\alpha e^{-\alpha c}$, so:

$$
A(c) = -\frac{-\alpha e^{-\alpha c}}{e^{-\alpha c}} = \alpha
$$

Absolute risk aversion is *constant* — it does not depend on wealth. This has a powerful implication: **a CARA agent's demand for risky assets is independent of her wealth level**. If she becomes richer, she does not shift any wealth into or out of the risky asset. This is a strong and empirically questionable prediction.

On the other hand, CARA utility is mathematically convenient. When returns are normally distributed, the expected utility of a CARA agent simplifies beautifully:

$$
\mathbb{E}[-e^{-\alpha \tilde{c}}] = -e^{-\alpha \mu + \frac{1}{2}\alpha^2 \sigma^2}
$$

Maximizing expected utility is then equivalent to maximizing $\mu - \frac{\alpha}{2}\sigma^2$ — the familiar mean-variance objective. This is the rigorous foundation of mean-variance analysis: it holds *exactly* under CARA utility with normal returns, and approximately otherwise.

### 3.2 Constant Relative Risk Aversion (CRRA): The Power Function

$$
u(c) = \begin{cases} \dfrac{c^{1-\gamma}}{1-\gamma} & \gamma \neq 1 \\ \ln(c) & \gamma = 1 \end{cases}
$$

Computing: $u'(c) = c^{-\gamma}$ and $u''(c) = -\gamma c^{-\gamma - 1}$, so:

$$
R(c) = -\frac{u''(c) \cdot c}{u'(c)} = -\frac{-\gamma c^{-\gamma-1} \cdot c}{c^{-\gamma}} = \gamma
$$

Relative risk aversion is constant and equal to $\gamma$. This is **the workhorse utility function in asset pricing**. It is used in virtually every consumption-based model, including the canonical Lucas (1978) economy and its descendants.

The parameter $\gamma$ has a clear economic interpretation as relative risk aversion, but it also governs the agent's **elasticity of intertemporal substitution (EIS)**, which equals $1/\gamma$ under CRRA. This creates a tension: empirically, we might want high risk aversion (large $\gamma$) to explain equity premia, but high $\gamma$ also implies low EIS, meaning agents strongly prefer smooth consumption over time. This tension is at the heart of the **equity premium puzzle**, which we will study in detail in Block 3.

The log utility case ($\gamma = 1$) is special and elegant. It can be shown that a log utility investor always invests a fixed fraction of wealth in each asset — optimal portfolio weights are independent of wealth and of the investment horizon.

### 3.3 Summary Table

| Utility | $u(c)$ | $A(c)$ | $R(c)$ | Key Property |
|---|---|---|---|---|
| Exponential (CARA) | $-e^{-\alpha c}/\alpha$ | $\alpha$ (constant) | $\alpha c$ (increasing) | Risky asset demand independent of wealth |
| Power (CRRA) | $c^{1-\gamma}/(1-\gamma)$ | $\gamma/c$ (decreasing) | $\gamma$ (constant) | Optimal portfolio shares independent of wealth |
| Quadratic | $c - \frac{b}{2}c^2$ | $b/(1-bc)$ | $bc/(1-bc)$ | Mean-variance exact; satiation at $c=1/b$ |
| Log | $\ln(c)$ | $1/c$ | $1$ | Myopic optimality, Kelly criterion |

---

## 4. Decreasing, Constant, and Increasing Risk Aversion

Whether $A(w)$ is decreasing, constant, or increasing in wealth has immediate behavioral implications.

**Decreasing Absolute Risk Aversion (DARA)**: $A'(w) < 0$. As the agent becomes wealthier, she is willing to bear more *dollar* risk. This is broadly consistent with empirical evidence — wealthy individuals hold more risky assets in dollar terms. CRRA utility satisfies DARA.

**Decreasing Relative Risk Aversion (DRRA)**: $R'(w) < 0$. The agent's *portfolio share* in risky assets rises with wealth. This is more controversial empirically; some studies find roughly constant relative risk aversion.

**Constant Relative Risk Aversion**: The risky portfolio share is independent of wealth. This is the CRRA case, and it is the most analytically tractable assumption consistent with balanced growth.

For asset pricing purposes, the most important fact is that CRRA is the *unique* utility function consistent with a stationary equilibrium in a growing economy. If aggregate consumption grows at a constant rate, we need preferences such that the agent's behavior does not drift over time — which requires constant relative risk aversion. This is a deep reason why CRRA dominates theoretical work.

---

## 5. Stochastic Dominance: Ranking Distributions Without a Utility Function

So far, risk aversion has been defined relative to a specific utility function. But sometimes we want to say that one lottery is "unambiguously better" than another — that *all* risk-averse agents prefer it, regardless of the specific shape of $u$.

This is the concept of **stochastic dominance**.

### First-Order Stochastic Dominance (FSD)

Lottery $F$ first-order stochastically dominates lottery $G$ if:

$$
F(x) \leq G(x) \quad \text{for all } x
$$

where $F$ and $G$ are the cumulative distribution functions. Intuitively, $F$ puts more probability weight on high outcomes: for any threshold $x$, the probability of falling below $x$ is lower under $F$.

**Theorem**: $F$ FSD $G$ if and only if $\mathbb{E}_F[u] \geq \mathbb{E}_G[u]$ for all *increasing* $u$.

FSD requires only that the agent prefers more to less — no assumption on risk aversion is needed.

### Second-Order Stochastic Dominance (SSD)

Lottery $F$ second-order stochastically dominates lottery $G$ if:

$$
\int_{-\infty}^{x} F(t) \, dt \leq \int_{-\infty}^{x} G(t) \, dt \quad \text{for all } x
$$

**Theorem**: $F$ SSD $G$ if and only if (i) $\mathbb{E}_F[X] = \mathbb{E}_G[X]$ and (ii) $\mathbb{E}_F[u] \geq \mathbb{E}_G[u]$ for all increasing *and concave* $u$.

SSD captures mean-preserving spreads: $G$ is $F$ with added noise. Any risk-averse agent (with concave $u$) prefers the less noisy distribution.

**Why does this matter for asset pricing?** Stochastic dominance gives us a model-free way to think about efficiency. If one portfolio SSD-dominates another with the same expected return, no risk-averse investor would hold the dominated one. In equilibrium, dominated portfolios cannot be held — which implies that observed portfolios must lie on the mean-variance frontier (under normality, where SSD and mean-variance efficiency coincide).

---

## 6. Risk Aversion and the Price of Risk

We close this block by connecting risk aversion back to prices — foreshadowing the full stochastic discount factor framework we will develop in Block 2.

Consider an agent with initial wealth $w_0$ who can invest a fraction $\alpha$ in a risky asset with return $\tilde{R}$ and the rest at the risk-free rate $R_f$. Her terminal wealth is:

$$
\tilde{w} = w_0 \left[ R_f + \alpha (\tilde{R} - R_f) \right]
$$

The first-order condition for the optimal $\alpha$ is:

$$
\mathbb{E}\left[ u'(\tilde{w}) \cdot (\tilde{R} - R_f) \right] = 0
$$

This is the **Euler equation** in its embryonic form. It says: at the optimum, the agent is indifferent at the margin between the risk-free asset and the risky one. The expected excess return must be zero when weighted by marginal utility.

Expanding this condition reveals something fundamental. Using $\text{Cov}(X, Y) = \mathbb{E}[XY] - \mathbb{E}[X]\mathbb{E}[Y]$:

$$
\mathbb{E}[u'(\tilde{w})] \cdot \mathbb{E}[\tilde{R} - R_f] + \text{Cov}(u'(\tilde{w}), \tilde{R} - R_f) = 0
$$

Rearranging:

$$
\mathbb{E}[\tilde{R}] - R_f = -\frac{\text{Cov}(u'(\tilde{w}), \tilde{R})}{\mathbb{E}[u'(\tilde{w})]}
$$

The expected excess return — the equity premium — equals the negative covariance between marginal utility and the return, normalized by expected marginal utility. Assets that pay off when marginal utility is high (when the agent is poor, when times are bad) have *low* expected returns, because they are insurance. Assets that pay off when marginal utility is low (when the agent is rich, when times are good) must offer *high* expected returns to be held.

This is the seed of the entire stochastic discount factor (SDF) theory. The SDF is $m \propto u'(\tilde{w})$, and every asset pricing model is fundamentally a model of what drives fluctuations in $m$. We will formalize this in Block 2.

---

## Key Takeaways

**Risk aversion is curvature.** An agent is risk averse if and only if her Bernoulli utility function is strictly concave. The certainty equivalent lies below the expected value, and the gap is the risk premium.

**Arrow-Pratt measures quantify risk aversion.** The coefficients $A(w) = -u''/u'$ (absolute) and $R(w) = -wu''/u'$ (relative) give local, cardinal measures of risk aversion that are independent of affine transformations of $u$.

**CRRA is the workhorse.** Power utility with constant relative risk aversion $\gamma$ is analytically tractable, consistent with balanced growth, and the foundation of modern consumption-based asset pricing. The parameter $\gamma$ simultaneously governs risk aversion and (inversely) the elasticity of intertemporal substitution.

**Stochastic dominance orders distributions without specifying $u$.** FSD (all agents prefer $F$) requires only monotonicity; SSD (all risk-averse agents prefer $F$ in a mean-preserving sense) requires concavity.

**Risk aversion generates expected return differences.** From the Euler equation, assets that covary negatively with marginal utility must offer positive expected returns. This is the fundamental logic that Block 2 will formalize into the SDF framework.

---

## Looking Ahead: Block 1.3 — Intertemporal Choice

We have now characterized how an agent values a single uncertain payoff. But most decisions in finance involve *sequences* of payoffs over time — savings decisions, portfolio rebalancing, consumption smoothing over a lifetime. 

Block 1.3 introduces the **intertemporal utility framework**: how preferences over time streams are represented by a discount factor $\beta$, why agents discount the future, and how the tension between time preference and risk aversion shapes the fundamental asset pricing equations. We will build up to the **Fisher equation** (the link between real interest rates and impatience) and arrive at the doorstep of the **consumption Euler equation** — the dynamic extension of the first-order condition we derived above.

---

*Block 1.1 — Preferences and Utility | **Block 1.2 — Risk Aversion** | Block 1.3 — Intertemporal Choice →*
