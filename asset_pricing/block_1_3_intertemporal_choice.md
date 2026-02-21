# Block 1.3 — Intertemporal Choice: Time, Patience, and the Price of Waiting

> *"A bird in the hand is worth two in the bush — but how many in the bush exactly, and why?"*

---

## Where We Left Off

Block 1.2 gave us the tools to value a single uncertain payoff. We characterized risk aversion through the curvature of the Bernoulli utility function $u(\cdot)$, derived the Arrow-Pratt measures, and arrived at the embryonic Euler equation:

$$
\mathbb{E}\left[ u'(\tilde{w}) \cdot (\tilde{R} - R_f) \right] = 0
$$

This is a *static* optimality condition — it tells us how to split wealth between assets at a single point in time. But most decisions in finance are inherently dynamic. A household decides how much to consume today and how much to save for tomorrow, and it does so repeatedly over a lifetime. An investor rebalances her portfolio every period as new information arrives. A firm issues bonds that promise payments decades into the future.

To handle these problems, we need preferences defined not just over a single outcome but over **sequences of consumption** across time. This block builds that framework — from the simplest two-period model to the full infinite-horizon recursive structure — and arrives at the **consumption Euler equation**, the central equation of modern dynamic asset pricing.

---

## 1. The Two-Period Model: A First Pass

Start with the simplest dynamic problem. An agent lives for two periods, $t = 0$ and $t = 1$. She has initial wealth $w_0$, consumes $c_0$ today, saves $s = w_0 - c_0$, earns a gross return $R$ on her savings, and consumes $c_1 = R \cdot s$ tomorrow. There is no uncertainty for now.

Her preferences over the consumption pair $(c_0, c_1)$ are represented by:

$$
U(c_0, c_1) = u(c_0) + \beta \, u(c_1)
$$

The parameter $\beta \in (0, 1)$ is the **subjective discount factor**. It captures the agent's pure time preference: even if $c_0 = c_1$, she values a unit of consumption today more than a unit tomorrow, simply because of impatience. The reciprocal $1/\beta$ is sometimes called the **subjective gross rate of time preference**, and $\delta = (1-\beta)/\beta$ is the **rate of time preference** (or impatience rate).

The agent maximizes $U$ subject to her budget constraint. Substituting:

$$
\max_{c_0} \; u(c_0) + \beta \, u\big(R(w_0 - c_0)\big)
$$

The first-order condition is:

$$
u'(c_0) = \beta R \, u'(c_1)
$$

This is the **consumption Euler equation** in its simplest deterministic form. Read it carefully: at the optimum, the marginal utility of consuming one more euro today equals the discounted, return-augmented marginal utility of the future consumption that saving one euro today would generate. The agent equates the marginal cost of waiting (losing $u'(c_0)$) to the marginal benefit (gaining $\beta R \, u'(c_1)$).

### The Fisher Equation

The Euler equation immediately delivers a connection between interest rates and preferences. Under log utility, $u'(c) = 1/c$, so:

$$
\frac{1}{c_0} = \beta R \cdot \frac{1}{c_1} \quad \Longrightarrow \quad R = \frac{1}{\beta} \cdot \frac{c_1}{c_0}
$$

If consumption is expected to grow at rate $g$ (so $c_1 = (1+g)c_0$), then:

$$
R = \frac{1+g}{\beta} \approx (1 + \delta)(1 + g) \approx 1 + \delta + g
$$

or in continuous time:

$$
r = \delta + g
$$

This is the **Fisher equation**: the real interest rate equals the rate of time preference plus the growth rate of consumption. It has a clear economic logic — in a growing economy, future consumption is relatively abundant, so its marginal utility is low, and the interest rate (which governs the intertemporal price) must be high enough to make the agent willing to save at all.

With CRRA utility ($u'(c) = c^{-\gamma}$), the Euler equation gives:

$$
c_0^{-\gamma} = \beta R \, c_1^{-\gamma} \quad \Longrightarrow \quad R = \frac{1}{\beta} \left(\frac{c_1}{c_0}\right)^{\gamma}
$$

The interest rate now depends on both the growth rate of consumption *and* risk aversion $\gamma$. When $\gamma$ is large, the agent strongly dislikes a falling consumption path and requires a high interest rate to be induced to save. In continuous time:

$$
r = \delta + \gamma g
$$

This is the **Ramsey rule**, the cornerstone of optimal growth theory and long-run discounting in environmental economics. The $\gamma g$ term is the **wealth effect**: fast consumption growth means marginal utility falls quickly, so future goods are relatively cheap, and the interest rate must rise to maintain indifference between present and future.

---

## 2. Uncertainty: The Stochastic Euler Equation

Now reintroduce uncertainty. The agent lives for two periods. At $t=0$, she chooses $c_0$ and saves $s = w_0 - c_0$. At $t=1$, a state of the world $s$ is realized, and her return is $R_s$, giving consumption $c_{1,s} = R_s \cdot s$. Her preferences are:

$$
U = u(c_0) + \beta \, \mathbb{E}_0[u(c_1)]
$$

where $\mathbb{E}_0[\cdot]$ is the expectation at time 0 over all possible states at time 1.

The first-order condition for optimal saving is:

$$
u'(c_0) = \beta \, \mathbb{E}_0\left[ R_1 \cdot u'(c_1) \right]
$$

More generally, if there are multiple assets $i$ each with gross return $R_{i,1}$, each must satisfy:

$$
\boxed{u'(c_0) = \beta \, \mathbb{E}_0\left[ R_{i,1} \cdot u'(c_1) \right]}
$$

Or, dividing both sides by $u'(c_0)$:

$$
1 = \mathbb{E}_0\left[ \beta \frac{u'(c_1)}{u'(c_0)} \cdot R_{i,1} \right]
$$

Define the **stochastic discount factor** (SDF):

$$
\boxed{m_1 \equiv \beta \frac{u'(c_1)}{u'(c_0)}}
$$

and the pricing equation becomes:

$$
1 = \mathbb{E}_0[m_1 \cdot R_{i,1}]
$$

or equivalently, for any asset with payoff $x_{i,1}$ and price $p_{i,0}$:

$$
p_{i,0} = \mathbb{E}_0[m_1 \cdot x_{i,1}]
$$

This is one of the most important equations in all of finance. **Every asset's price is the expected value of its payoff, discounted by the stochastic discount factor.** The SDF is not a constant discount rate — it is a random variable that fluctuates with the state of the world, high when consumption is low and marginal utility is high, low when the economy is booming. Block 2 will be devoted entirely to exploring this equation. For now, we note that it emerges naturally from the intertemporal optimization of a risk-averse agent.

---

## 3. The Infinite-Horizon Problem

Two-period models are pedagogically useful but economically limiting. Most serious models of asset pricing assume agents live forever (or equivalently, that they care about their descendants). The infinite-horizon problem is:

$$
\max_{\{c_t\}_{t=0}^{\infty}} \; \mathbb{E}_0 \left[ \sum_{t=0}^{\infty} \beta^t u(c_t) \right]
$$

subject to a sequence of budget constraints. For this sum to be well-defined and finite, we need $\beta < 1$ (the future is discounted) and the utility function to be bounded, or consumption to not grow too fast.

The key insight is that this problem is **time-consistent** and **recursive**. The agent's problem looks identical at every point in time: maximize the present discounted value of future utility from that point onward. This allows us to write the problem in a much more compact form.

### The Bellman Equation

Define the **value function** $V(w_t)$ as the maximum expected utility the agent can achieve starting at time $t$ with wealth $w_t$:

$$
V(w_t) = \max_{c_t} \left\{ u(c_t) + \beta \, \mathbb{E}_t[V(w_{t+1})] \right\}
$$

This is the **Bellman equation**. It decomposes the infinite-horizon problem into a two-period problem: the agent chooses how much to consume today, trading off current utility $u(c_t)$ against the discounted continuation value $\beta \mathbb{E}_t[V(w_{t+1})]$.

The elegance is that the same Euler equation as before characterizes the optimum at every date:

$$
u'(c_t) = \beta \, \mathbb{E}_t\left[ R_{t+1} \cdot u'(c_{t+1}) \right]
$$

This holds for every $t$ simultaneously. The agent is always on the margin between consuming today and investing to consume tomorrow. The whole sequence of future consumption adjusts so that this condition holds at every date and in every state.

### The Transversality Condition

The Euler equation is necessary but not sufficient for an optimum in infinite horizon problems. We also need the **transversality condition**:

$$
\lim_{T \to \infty} \beta^T \, \mathbb{E}_0[u'(c_T) \cdot w_T] = 0
$$

Intuitively, this rules out "Ponzi schemes" — plans where the agent accumulates infinite debt that is never repaid, or conversely, plans where the agent saves infinitely without ever consuming. The agent must eventually run down her wealth. Without this condition, there would be multiple paths satisfying the Euler equation, many of which are clearly non-optimal.

---

## 4. Time Preference and the Discount Factor

Let us pause to think more carefully about the discount factor $\beta$ and what it represents.

### Impatience as a Primitive

The discount factor $\beta$ is often justified by three distinct arguments:

**Pure time preference**: People simply prefer present consumption to future consumption, even when both are certain and equal. This is a primitive preference, sometimes criticized as irrational (why should tomorrow's consumption matter less?) but empirically robust. Ramsey (1928) famously called pure time preference "a polite expression for the weakness of the imagination."

**Probability of survival**: In a finite-lifetime model, $\beta$ can reflect the probability that the agent survives to consume tomorrow. If death arrives with probability $1 - p$ each period, the agent effectively discounts future utility by $p$, giving $\beta = p$. This provides a biological microfoundation for discounting.

**Preference for flexibility**: Future commitments are less valuable than present ones because circumstances may change. A discount factor can emerge from a preference for keeping options open.

In practice, empirical estimates of $\beta$ in annual data cluster around $0.94$–$0.99$, implying rates of time preference of $1$–$6\%$ per year. The exact value matters enormously for long-horizon problems like climate policy or pension design, which is why the "right" discount rate is fiercely debated.

### Hyperbolic Discounting

The exponential discounting model $\beta^t$ has a key property: **time consistency**. A plan that seems optimal today also seems optimal tomorrow, once tomorrow arrives. The relative valuation of any two future dates does not change as time passes.

Empirical evidence, however, suggests that people exhibit **present bias**: they are disproportionately impatient about the near future relative to the distant future. A typical pattern: given the choice between €100 today and €110 tomorrow, people often prefer €100 today; but given the choice between €100 in 30 days and €110 in 31 days, they prefer €110 in 31 days. The one-day delay feels different depending on when it occurs.

This is captured by **hyperbolic discounting**, where the discount factor between today and $t$ periods ahead is $(1 + kt)^{-1}$ for some $k > 0$, rather than $\beta^t$. Hyperbolic discounting generates time-inconsistent preferences: agents make plans they later abandon, save less than they intend, and procrastinate. While not the standard assumption in asset pricing models, it has generated a rich literature in behavioral finance and public economics.

For the rest of this course, we maintain the exponential discounting assumption for its tractability and time-consistency, while acknowledging it is a simplification.

---

## 5. Consumption Smoothing and the Interest Rate

The Euler equation has an important implication that is sometimes underappreciated: it tells us that the **expected growth rate of consumption** is determined by the interest rate and preferences, not by income shocks per se.

Rewrite the CRRA Euler equation as:

$$
\mathbb{E}_t\left[\beta R_{t+1} \left(\frac{c_{t+1}}{c_t}\right)^{-\gamma}\right] = 1
$$

Under log-normality of consumption growth (a standard approximation), taking logs and using the log-normal moment formula $\ln \mathbb{E}[e^X] = \mathbb{E}[X] + \frac{1}{2}\text{Var}(X)$, this gives:

$$
\ln R_f = -\ln \beta + \gamma \, \mathbb{E}_t[\Delta \ln c_{t+1}] - \frac{\gamma^2}{2} \text{Var}_t(\Delta \ln c_{t+1})
$$

where $R_f$ is the risk-free gross return and $\Delta \ln c_{t+1} = \ln c_{t+1} - \ln c_t$ is consumption growth. Rearranging:

$$
\mathbb{E}_t[\Delta \ln c_{t+1}] = \frac{1}{\gamma}\left(r_f + \delta\right) - \frac{\gamma}{2}\sigma_c^2
$$

where $r_f = \ln R_f$, $\delta = -\ln\beta$, and $\sigma_c^2 = \text{Var}_t(\Delta \ln c_{t+1})$.

Several things follow immediately:

**Higher real interest rates raise expected consumption growth.** When the return on saving rises, the agent shifts consumption toward the future. The magnitude of this response is governed by $1/\gamma$, which is exactly the **elasticity of intertemporal substitution (EIS)**. High $\gamma$ (high risk aversion, low EIS) means consumption growth is barely responsive to interest rates — the agent strongly wants a smooth consumption path and adjusts little.

**Higher consumption volatility lowers expected consumption growth.** The $-\frac{\gamma}{2}\sigma_c^2$ term is the **precautionary savings effect**: uncertainty about future consumption induces the agent to save more (consume less today), generating higher future expected consumption. This precautionary motive is a second-order effect, absent under quadratic utility, but important under CRRA for $\gamma > 1$.

---

## 6. The Equity Premium Puzzle: A First Glimpse

We close this block with a famous puzzle that the intertemporal framework immediately generates. It will motivate much of the rest of the course.

The consumption Euler equation for an equity claim with return $R^e$ and the risk-free asset gives:

$$
\mathbb{E}_t[R^e_{t+1}] - R_f = -R_f \cdot \text{Cov}_t\left(m_{t+1}, R^e_{t+1}\right)
$$

where $m_{t+1} = \beta (c_{t+1}/c_t)^{-\gamma}$. Using $\text{Cov}(m, R^e) = \rho_{m,R^e} \cdot \sigma_m \cdot \sigma_{R^e}$:

$$
\frac{\mathbb{E}_t[R^e_{t+1}] - R_f}{\sigma_{R^e}} = -\rho_{m,R^e} \cdot \frac{\sigma_m}{\mathbb{E}[m]}
$$

The left-hand side is the **Sharpe ratio** of equity — the excess return per unit of return volatility. The right-hand side involves $\sigma_m / \mathbb{E}[m]$, the **coefficient of variation of the SDF**.

Mehra and Prescott (1985) showed that historical US data implies a Sharpe ratio for equity of about $0.5$. Under the consumption-based model with CRRA utility, $\sigma_m/\mathbb{E}[m] \approx \gamma \sigma_c$, where $\sigma_c \approx 1\%$ is the annual standard deviation of per-capita consumption growth. To match the observed Sharpe ratio:

$$
\gamma \cdot 0.01 \geq 0.5 \quad \Longrightarrow \quad \gamma \geq 50
$$

A coefficient of relative risk aversion of 50 is wildly implausible — it implies, for example, that an agent would refuse a 50/50 gamble between doubling her consumption and a 2% reduction. Most calibration exercises and experimental evidence suggest $\gamma \in [1, 10]$.

This is the **equity premium puzzle**: the observed premium on equities is far too large to be explained by the observed volatility of consumption growth, under any reasonable level of risk aversion. It is not a minor quantitative discrepancy — it is an order-of-magnitude failure of the benchmark model.

We will return to this puzzle repeatedly. Proposed resolutions include habit formation (Block 4), recursive preferences that separate risk aversion from EIS (Block 5), rare disasters, long-run risks, and limited market participation. Each resolution modifies some ingredient of the framework we have built in these first three blocks. Understanding the puzzle deeply requires having the framework firmly in hand — which is now the case.

---

## Key Takeaways

**The discount factor $\beta$ captures time preference.** Agents prefer present consumption to future consumption. The Euler equation equates the marginal utility of consuming today to the discounted, return-adjusted marginal utility of consuming tomorrow.

**The Fisher/Ramsey rule connects real interest rates, impatience, and growth.** In a deterministic CRRA economy: $r = \delta + \gamma g$. Higher growth raises interest rates; higher risk aversion amplifies the effect.

**The stochastic discount factor emerges naturally.** Defining $m_{t+1} = \beta u'(c_{t+1})/u'(c_t)$, every asset satisfies $1 = \mathbb{E}_t[m_{t+1} R_{i,t+1}]$. This is the master equation of asset pricing.

**The EIS governs consumption smoothing.** Under CRRA, the elasticity of intertemporal substitution is $1/\gamma$. It controls how strongly the agent shifts consumption in response to interest rate changes, distinct from how she responds to risk.

**The equity premium puzzle reveals the tension at the heart of the model.** Matching observed asset prices requires implausibly high risk aversion. Resolving this tension is the central challenge — and central achievement — of modern asset pricing theory.

---

## Looking Ahead: Block 2 — The Stochastic Discount Factor

We have now arrived at the frontier of what the preference-based foundations can deliver on their own. The next block takes the equation $p_t = \mathbb{E}_t[m_{t+1} x_{t+1}]$ as its starting point and develops the **SDF framework** in full generality — without committing to a specific utility function or even to any consumption-based model.

The key questions will be: What restrictions does the absence of arbitrage alone place on $m$? What does the SDF look like in complete versus incomplete markets? And how does the SDF relate to the familiar tools of mean-variance analysis and the CAPM? The answers will give us a unified language for thinking about *all* asset pricing models — a language in which every model is simply a specific parametrization of the SDF.

---

*Block 1.2 — Risk Aversion | **Block 1.3 — Intertemporal Choice** | Block 2.1 — The SDF Framework →*
