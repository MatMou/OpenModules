# Asset Pricing from Scratch

# Part I — Foundations: Discrete Time, Finite States

# Section 1: Decision Under Uncertainty

## Block 1.1 — Preferences and Utility

---

### The Question That Starts Everything

Asset pricing is about determining the value of uncertain future payoffs. A stock might pay dividends or crash. A bond might default. An insurance contract pays only if disaster strikes. Before we can say what any of these are *worth*, we need to answer a more primitive question:

> **How do people choose when the future is uncertain?**

This is not a question about markets. There are no prices yet, no portfolios, no equilibrium. It is a question about a single individual facing a set of risky prospects and having to rank them. Get this wrong, and nothing downstream — no CAPM, no Black-Scholes, no stochastic discount factor — has any foundation.

So the entire theory of asset pricing begins here, with a person standing in front of a choice.

---

### The Problem of Ranking Gambles

Suppose you are offered two job contracts:

- **Job A**: pays €80,000 per year, guaranteed.
- **Job B**: pays €150,000 with probability 1/2, and €30,000 with probability 1/2.

Job B has a higher expected income: $\frac{1}{2}(150{,}000) + \frac{1}{2}(30{,}000) = 90{,}000 > 80{,}000$. Yet most people, when actually confronted with this choice, prefer A — or at the very least, they hesitate. The guaranteed salary feels safer. The possibility of earning only €30,000 looms larger than the possibility of €150,000.

This simple observation has a profound consequence: **people do not maximize expected payoffs**. If they did, everyone would pick B without a second thought. Something else is going on. People care about the *shape* of the distribution of outcomes — how spread out it is, how bad the worst case is — not just the average.

Any useful theory of choice under uncertainty must capture this. We need a framework that:

1. Allows agents to rank *any* pair of risky prospects (not just those with obvious dominance).
2. Explains why agents might sacrifice expected payoff for reduced risk.
3. Is mathematically tractable enough to plug into pricing models.

The framework that achieves all three is **Expected Utility Theory**, developed by John von Neumann and Oskar Morgenstern in 1944.

---

### Lotteries: The Language of Uncertain Prospects

Before stating any axioms, we need a precise language for what agents are choosing between. The concept is the **lottery**.

A **lottery** $L$ is a probability distribution over a set of outcomes. In the simplest case, outcomes are monetary payoffs $x_1, x_2, \ldots, x_n$ received with probabilities $p_1, p_2, \ldots, p_n$, where $p_i \geq 0$ and $\sum_i p_i = 1$. We write:

$$L = (x_1, p_1; \; x_2, p_2; \; \ldots; \; x_n, p_n)$$

Job A above is a **degenerate lottery**: $(80{,}000, \; 1)$. Job B is $(150{,}000, \; 0.5; \; 30{,}000, \; 0.5)$.

We can also form **compound lotteries**. Suppose you flip a coin: heads you play lottery $L_1$, tails you play lottery $L_2$. The compound lottery is $\frac{1}{2}L_1 + \frac{1}{2}L_2$. More generally, for any $\alpha \in [0,1]$, the mixture $\alpha L_1 + (1-\alpha) L_2$ is the lottery that plays $L_1$ with probability $\alpha$ and $L_2$ with probability $1-\alpha$.

Let $\mathcal{L}$ denote the set of all lotteries over a given outcome space. The agent has preferences over $\mathcal{L}$: a binary relation $\succeq$ where $L_1 \succeq L_2$ means "the agent weakly prefers $L_1$ to $L_2$." From this we derive strict preference ($L_1 \succ L_2$ if $L_1 \succeq L_2$ but not $L_2 \succeq L_1$) and indifference ($L_1 \sim L_2$ if both $L_1 \succeq L_2$ and $L_2 \succeq L_1$).

The question is: **what structure should $\succeq$ have?**

---

### The von Neumann–Morgenstern Axioms

Von Neumann and Morgenstern did not *assume* a formula for how people evaluate lotteries. Instead, they asked: what minimal requirements should we impose on rational preferences? They proposed four axioms. Each is intuitively appealing, and together they have remarkably powerful consequences.

---

#### Axiom 1 — Completeness

> For any two lotteries $L_1, L_2 \in \mathcal{L}$, either $L_1 \succeq L_2$, or $L_2 \succeq L_1$, or both.

The agent can always make a comparison. There is no pair of gambles that leaves them paralyzed, unable to say which they prefer (or that they are indifferent). This is a strong assumption — in practice, people sometimes genuinely don't know how to rank two complex prospects — but it is the minimal requirement for preferences to be useful as an input to a mathematical model.

Without completeness, we cannot define a demand function, because the agent might face a menu of assets and be unable to choose.

---

#### Axiom 2 — Transitivity

> If $L_1 \succeq L_2$ and $L_2 \succeq L_3$, then $L_1 \succeq L_3$.

Preferences don't cycle. If you prefer apples to bananas and bananas to cherries, you prefer apples to cherries.

This sounds trivial, but it has teeth. An agent with intransitive preferences can be **money-pumped**: a clever counterparty can offer a sequence of trades, each of which the agent willingly accepts, that extract unlimited wealth from the agent. Suppose the agent has $A \succ B \succ C \succ A$ (a cycle). Start with $A$. The agent prefers $C$ to $A$, so they'll pay a small fee to switch. Now they have $C$. They prefer $B$ to $C$, so they'll pay again. Now they have $B$. They prefer $A$ to $B$, so they pay a third time — and they're back where they started, but poorer. Repeat indefinitely.

Transitivity is what prevents exploitation. It is the axiom that makes the agent a coherent decision-maker rather than a source of free money for others.

---

#### Axiom 3 — Continuity (the Archimedean Axiom)

> If $L_1 \succeq L_2 \succeq L_3$, then there exists some $\alpha \in [0,1]$ such that:
> $$L_2 \sim \alpha L_1 + (1-\alpha) L_3$$

The agent is indifferent between $L_2$ and some mixture of the best ($L_1$) and worst ($L_3$) lotteries. In other words, you can always compensate for a worse lottery by mixing in enough of a better one.

This rules out **lexicographic preferences** — situations where one dimension of a lottery is infinitely more important than another. For instance, suppose $L_1$ is "live and receive €1," $L_2$ is "live and receive €0," and $L_3$ is "die." A person with lexicographic preferences over survival might say: no probability of death, no matter how small, can compensate for any monetary gain. They would prefer $L_2$ to any mixture $\alpha L_1 + (1-\alpha)L_3$ for every $\alpha < 1$. This violates continuity.

Most people do in fact accept tiny risks of death for monetary compensation (driving to work, for instance), so continuity is empirically plausible for most choices. But it is worth noting: **the axiom has a price**. It forces all outcomes to be commensurable — tradeable against one another at some rate.

Continuity is technically necessary to guarantee that preferences can be represented by a *real-valued* function. Without it, we might need something richer than the real number line to encode the preference ordering.

---

#### Axiom 4 — Independence

> If $L_1 \succeq L_2$, then for any lottery $L_3$ and any $\alpha \in (0,1]$:
> $$\alpha L_1 + (1-\alpha) L_3 \succeq \alpha L_2 + (1-\alpha) L_3$$

This is the most important and most debated axiom. It says: if you prefer $L_1$ to $L_2$, then mixing both with a common third lottery $L_3$ does not reverse your ranking. The "irrelevant" lottery $L_3$ is just background noise — it washes out.

Think of it this way. You prefer chocolate ice cream to vanilla. Now I tell you: with probability $\alpha$, you get to choose between chocolate and vanilla; with probability $(1-\alpha)$, you get strawberry regardless. Independence says: you still prefer chocolate in the $\alpha$-branch. The possibility of strawberry in the other branch shouldn't change your ranking of chocolate vs. vanilla.

**Why Independence is powerful.** It is the axiom that rules out preferences depending on the "global shape" of the lottery. It forces the evaluation of a lottery to decompose additively across outcomes — which is what leads to the *expected* utility representation. Without it, you could have preferences that depend on correlations between different parts of the gamble, on disappointment relative to what might have been, or on the context in which the lottery is framed.

**Why Independence is controversial: the Allais Paradox.** In 1953, Maurice Allais constructed the following experiment. Consider four lotteries:

| | Lottery A | Lottery B |
|---|---|---|
| Choice 1 | €1M with certainty | €5M (10%), €1M (89%), €0 (1%) |
| Choice 2 | €1M (11%), €0 (89%) | €5M (10%), €0 (90%) |

Most people choose $A$ over $B$ in Choice 1 (they prefer the sure million) and $D$ over $C$ in Choice 2 (the probabilities are so low anyway that they go for the bigger prize). But this pair of choices violates Independence. To see why, note that Choice 1 and Choice 2 have the same structure: they differ only in whether an 89% "common consequence" pays €1M or €0. Independence says this common consequence shouldn't matter — so if you prefer $A$ to $B$, you should also prefer $C$ to $D$.

The Allais paradox reveals that real human preferences are affected by the *certainty* of an outcome in a way that Independence forbids. This has led to alternative theories (prospect theory, rank-dependent utility) that relax Independence. But for the purposes of building asset pricing theory, we retain Independence as our benchmark of rationality. We will revisit its failures when we discuss behavioral finance.

---

### The Expected Utility Theorem

The four axioms are individually modest. Their joint consequence is extraordinary.

**Theorem (von Neumann–Morgenstern, 1944).** If the preference relation $\succeq$ over lotteries satisfies Completeness, Transitivity, Continuity, and Independence, then there exists a function $u: \mathbb{R} \to \mathbb{R}$ such that for any two lotteries $L_1$ and $L_2$:

$$L_1 \succeq L_2 \quad \Longleftrightarrow \quad \mathbb{E}[u(X_1)] \geq \mathbb{E}[u(X_2)]$$

where $X_1$ and $X_2$ are the random payoffs of $L_1$ and $L_2$, respectively.

Moreover, $u$ is **unique up to positive affine transformation**: if $u$ represents $\succeq$, then so does $v(x) = a \cdot u(x) + b$ for any constants $a > 0$ and $b \in \mathbb{R}$, and *only* such transformations of $u$ also represent $\succeq$.

---

#### What the theorem says (and what it doesn't)

**It is a representation result, not an assumption.** We did not assume that agents compute expected utilities. We assumed four properties of how they rank lotteries, and *derived* that their behavior is *as if* they maximize expected utility. The distinction matters: when the model fails empirically, we know which axiom to question, rather than having to discard the entire framework.

**The utility function transforms payoffs before expectations.** The agent evaluates $\mathbb{E}[u(X)]$, not $\mathbb{E}[X]$. The function $u$ encodes how the agent *feels* about different wealth levels. A person with a concave $u$ weights losses more heavily than equivalent gains — they are risk-averse. A person with a linear $u$ is risk-neutral and does simply maximize expected payoffs. The concavity of $u$ is doing all the work in explaining why people prefer Job A to Job B.

**Uniqueness up to affine transformation means cardinal utility (up to scale).** Unlike ordinal utility in consumer theory (where any monotone transformation preserves the ranking), here the *shape* of $u$ matters. Specifically, the curvature of $u$ carries information about risk attitudes. The intercept $b$ and scaling $a$ are arbitrary (like choosing between Celsius and Fahrenheit), but the concavity is intrinsic.

---

#### Sketch of the proof idea

The full proof is technical, but the intuition is clean and worth understanding, as it reveals *why* the axioms lead to expected utility.

**Step 1: Calibrate extreme outcomes.** By Continuity, for any lottery $L$ there exists a unique $\alpha_L \in [0,1]$ such that $L \sim \alpha_L L^* + (1 - \alpha_L) L_*$, where $L^*$ is the best lottery and $L_*$ is the worst. This $\alpha_L$ is a numerical "score" for every lottery.

**Step 2: Show the score is linear in mixtures.** Independence implies that the score of a compound lottery $\alpha L_1 + (1-\alpha)L_2$ is exactly $\alpha \cdot \alpha_{L_1} + (1-\alpha) \cdot \alpha_{L_2}$. That is, the score decomposes linearly across the components of a mixture. This is the algebraic fingerprint of the Independence axiom.

**Step 3: Identify the score with expected utility.** For a simple lottery $(x_1, p_1; \ldots; x_n, p_n)$, treat each outcome $x_i$ as a degenerate lottery with score $u(x_i) := \alpha_{x_i}$. By the linearity from Step 2, the score of the full lottery is $\sum_i p_i \cdot u(x_i) = \mathbb{E}[u(X)]$.

The entire theorem pivots on Step 2: the Independence axiom forces the evaluation functional to be *linear in probabilities*. This linearity in probabilities is the structural essence of expected utility, and everything that follows in asset pricing — from the existence of the stochastic discount factor to the first fundamental theorem — is, at root, a consequence of exploiting linearity.

---

### Why "Expected Utility" Is Not "Expected Value"

This point deserves emphasis because the confusion is common and consequential.

**Expected value** is $\mathbb{E}[X] = \sum_s \pi_s X_s$. It is a linear function of outcomes.

**Expected utility** is $\mathbb{E}[u(X)] = \sum_s \pi_s \, u(X_s)$. It is a linear function of *transformed* outcomes.

The transformation $u$ is everything. When $u$ is linear ($u(x) = ax + b$), expected utility reduces to expected value (up to constants), and the agent is risk-neutral. But when $u$ is concave, the agent penalizes bad outcomes more than they reward good ones. The non-linearity of $u$ is the source of risk premia, the demand for insurance, the existence of hedging, and ultimately the reason why assets with high covariance to bad times earn higher expected returns.

Consider two lotteries with the same expected payoff:

- $L_1$: pays €100 with certainty. $\mathbb{E}[X] = 100$.
- $L_2$: pays €200 with probability 0.5 and €0 with probability 0.5. $\mathbb{E}[X] = 100$.

With $u(x) = \sqrt{x}$ (a concave utility):

$$\mathbb{E}[u(L_1)] = \sqrt{100} = 10$$
$$\mathbb{E}[u(L_2)] = 0.5 \cdot \sqrt{200} + 0.5 \cdot \sqrt{0} = 0.5 \times 14.14 + 0 = 7.07$$

The agent strictly prefers $L_1$, even though both have the same expected payoff. The difference $10 - 7.07 = 2.93$ is the "utility cost" of bearing risk, and it will later translate into a price discount for risky assets.

---

### Looking Ahead

We now have a rigorous foundation: agents have preferences over lotteries, and if those preferences are rational (in the sense of the four axioms), they behave as if they maximize expected utility for some function $u$.

But we have not yet said anything about **what kind of $u$ generates what kind of behavior**. The next block — *Risk Aversion* — turns the spotlight on the curvature of $u$. We will see that concavity is equivalent to risk aversion, learn to measure its intensity (Arrow-Pratt coefficients), and catalog the specific utility functions that power the asset pricing literature. The risk premium — the quantity that ultimately drives asset prices — will emerge naturally as the gap between what a lottery is expected to pay and what a risk-averse agent is willing to pay for it.

---

### Key References

- **von Neumann, J. & Morgenstern, O.** (1944). *Theory of Games and Economic Behavior*. Princeton University Press. — The original source. Chapter 3 develops the axioms and the representation theorem.
- **Mas-Colell, A., Whinston, M.D. & Green, J.R.** (1995). *Microeconomic Theory*. Oxford University Press. Chapter 6. — The cleanest modern textbook treatment of expected utility.
- **Allais, M.** (1953). "Le comportement de l'homme rationnel devant le risque." *Econometrica*, 21(4), 503–546. — The original statement of the Allais paradox.
- **Machina, M.J.** (1987). "Choice Under Uncertainty: Problems Solved and Unsolved." *Journal of Economic Perspectives*, 1(1), 121–154. — An excellent survey of what works and what fails in expected utility theory.
- **Cochrane, J.H.** (2005). *Asset Pricing* (Revised Edition). Princeton University Press. Chapter 1. — The big picture of where preferences fit in asset pricing.
