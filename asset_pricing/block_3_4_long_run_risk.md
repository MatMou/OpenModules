# Block 3.4 — Long-Run Risk: The Fear of Persistent Shocks

> *"The key insight is simple but profound: if investors care about the long run, then small but persistent fluctuations in growth prospects can generate large risk premia — even when current consumption barely moves."*
> — Ravi Bansal and Amir Yaron, *Journal of Finance* (2004)

---

## Where We Left Off

Block 3.3 established the Epstein-Zin preference structure and derived its central implication for asset pricing: when the coefficient of relative risk aversion exceeds the reciprocal of the elasticity of intertemporal substitution ($\gamma > 1/\psi$), agents prefer early resolution of uncertainty and therefore price *news about the long-run future* as a distinct and separately compensated risk. The stochastic discount factor under Epstein-Zin preferences responds not only to current consumption growth but to the entire present value of revisions in long-run expected growth — a fundamentally richer pricing kernel than the CRRA model allows.

But Block 3.3 left a critical question open: what does the consumption process actually look like, and how large are the long-run risk components that this SDF is pricing? If expected consumption growth is constant — as in the Mehra-Prescott i.i.d. economy — then there is no long-run risk to price, and Epstein-Zin preferences reduce in effect to CRRA. The preferences alone cannot generate large risk premia; they must be combined with a consumption process that contains the kind of variation that these preferences are sensitive to.

Bansal and Yaron (2004) provided the missing piece. They proposed a consumption process with two key features: a **small but highly persistent** predictable component in expected growth, and **time-varying volatility** in consumption growth. Neither of these components is easily detectable in short samples of consumption data — both are quantitatively small relative to the short-run noise. But under Epstein-Zin preferences with high EIS, even tiny persistent fluctuations in expected growth generate large and time-varying risk premia, because the agent extrapolates these signals into revisions about all future consumption. The model matches not just the equity premium and risk-free rate but the volatility of returns, the behavior of the price-dividend ratio, the predictability of returns, and the variance of dividend growth — a remarkable breadth of empirical success that placed it at the center of the consumption-based asset pricing agenda for nearly two decades.

This block derives the Bansal-Yaron model in full, examines its calibration and mechanism in depth, assesses its empirical predictions, and discusses its limitations and the subsequent literature it spawned.

---

## 1. The Consumption and Dividend Process

### Motivation: What Is Long-Run Risk?

The empirical motivation for the long-run risk model begins with an observation about the time-series properties of consumption and dividend growth. While both series look approximately i.i.d. in short samples — consistent with the Mehra-Prescott assumption — longer-span data and more careful statistical analysis reveals slow-moving predictable components. Expected consumption growth is not constant: it varies with the business cycle, with monetary policy regimes, with demographic trends, and with the long-run prospects of productivity growth. These variations are small at quarterly or annual horizons but cumulate into large revisions over decades.

More precisely, Bansal and Yaron document that:
- Consumption growth is **slightly positively autocorrelated** at long horizons, inconsistent with i.i.d. growth.
- Consumption growth and dividend growth share a **common slow-moving component** — persistent shocks to fundamentals affect both simultaneously.
- **Return volatility is time-varying**: calm periods alternate with turbulent periods in ways that are not captured by constant-volatility models.

The long-run risk model formalizes these observations into a tractable continuous-time or discrete-time system. We focus on the discrete-time version, which is more directly connected to the empirical literature.

### The State-Space System

The Bansal-Yaron model specifies the following joint process for log consumption growth $\Delta c_{t+1} = \ln(C_{t+1}/C_t)$ and log dividend growth $\Delta d_{t+1} = \ln(D_{t+1}/D_t)$:

$$
\Delta c_{t+1} = \mu_c + x_t + \sigma_t \eta_{t+1}
$$

$$
\Delta d_{t+1} = \mu_d + \phi x_t + \varphi_d \sigma_t u_{t+1}
$$

$$
x_{t+1} = \rho x_t + \varphi_e \sigma_t e_{t+1}
$$

$$
\sigma^2_{t+1} = \bar{\sigma}^2 + \nu_1(\sigma^2_t - \bar{\sigma}^2) + \sigma_w w_{t+1}
$$

where $\eta_{t+1}$, $u_{t+1}$, $e_{t+1}$, and $w_{t+1}$ are mutually independent standard normal shocks.

Let us examine each equation carefully, as the structure carries important economic content.

**Consumption growth** ($\Delta c_{t+1}$): Log consumption growth has three components. The first is a constant mean $\mu_c$. The second is $x_t$ — the **long-run risk component**, a time-varying expected growth rate that is observable by agents but not by the econometrician (or at least not easily identifiable in short samples). The third is a contemporaneous noise term $\sigma_t \eta_{t+1}$ with time-varying volatility.

**Dividend growth** ($\Delta d_{t+1}$): Dividends share the long-run risk component $x_t$ with coefficient $\phi > 1$, which allows dividends to be riskier than consumption — consistent with the empirical finding that dividend growth is more volatile than consumption growth. The idiosyncratic dividend noise $u_{t+1}$ is orthogonal to consumption shocks, consistent with the idea that firm-specific decisions affect dividends but not aggregate consumption.

**The long-run risk process** ($x_{t+1}$): This is the central equation. $x_t$ follows an AR(1) with persistence coefficient $\rho$ close to (but strictly less than) one. The innovation $\varphi_e \sigma_t e_{t+1}$ has time-varying volatility, so shocks to expected growth are larger in volatile periods. The persistence $\rho \approx 0.979$ in the annual calibration — meaning the half-life of a shock to expected growth is approximately $0.979^{-1} \approx 33$ years. This is very persistent but not explosive.

**The volatility process** ($\sigma^2_{t+1}$): The conditional variance of consumption growth follows an AR(1) around its unconditional mean $\bar{\sigma}^2$, with persistence $\nu_1$ and volatility-of-volatility $\sigma_w$. This is the **stochastic volatility** component — the second source of long-run risk. When $\sigma^2_t$ is high, the economy is in a high-uncertainty regime; when it is low, growth is predictably smoother.

### The Two Sources of Long-Run Risk

The model therefore contains **two distinct long-run risks**:

**Type 1 — Long-run expected growth risk**: Shocks to $x_t$ alter expected consumption growth for many periods into the future. A negative shock to $x_t$ today reduces expected consumption growth for the next 30+ years. An agent who prices long-run prospects will view this as very bad news and demand a large premium for assets exposed to $x_t$ shocks.

**Type 2 — Long-run volatility risk**: Shocks to $\sigma^2_t$ alter the uncertainty of future consumption. A rise in $\sigma^2_t$ makes all future shocks larger, increasing uncertainty about long-run welfare. An agent who dislikes uncertainty about future uncertainty — whose utility function is sensitive to second-moment risk — will demand a premium for assets correlated with $\sigma^2_t$ shocks.

Under CRRA preferences, neither of these long-run risk components would generate much pricing impact: the CRRA SDF only responds to current consumption growth, which is the sum of the predictable part $x_t$ and noise $\sigma_t \eta_{t+1}$. The long-run components are simply too small to generate large risk premia in the static pricing framework. Under Epstein-Zin preferences with $\gamma > 1/\psi$, by contrast, both components are amplified enormously because the agent extrapolates shocks to $x_t$ and $\sigma^2_t$ into revisions about all future welfare — and it is the present value of all future welfare that drives the pricing kernel.

---

## 2. Asset Prices in the Long-Run Risk Model

### The Price-Dividend Ratio and the Wealth-Consumption Ratio

In the Bansal-Yaron model, asset prices are log-linear functions of the state variables $(x_t, \sigma^2_t)$. This follows from the log-linear approximation to the wealth-consumption ratio and the price-dividend ratio — a standard technique due to Campbell and Shiller (1988) that linearizes the exact but nonlinear present value recursion.

The **log price-dividend ratio** $z_t = \ln(P_t/D_t)$ can be written as:

$$
z_t = A_0 + A_1 x_t + A_2 \sigma^2_t
$$

The coefficients $A_1$ and $A_2$ are determined by the model's structural parameters. Their signs carry immediate economic intuition:

**$A_1 > 0$**: When expected growth $x_t$ is high, future dividends are expected to be large, and the price-dividend ratio rises. This is the cash flow channel: higher expected growth raises expected future dividends, which raises prices.

**$A_2 < 0$**: When volatility $\sigma^2_t$ is high, uncertainty is elevated. With $\gamma > 1/\psi$, the agent dislikes uncertainty and therefore demands higher expected returns, which — for a given dividend stream — means lower prices. The discount rate channel dominates: higher uncertainty raises discount rates and lowers the price-dividend ratio.

The coexistence of positive $A_1$ and negative $A_2$ generates rich price dynamics. When bad times feature both low $x_t$ (reduced expected growth) and high $\sigma^2_t$ (elevated uncertainty), the price-dividend ratio falls sharply through both channels simultaneously. This explains why stock market downturns are typically accompanied by spikes in uncertainty and revisions to long-run growth expectations — the model captures this joint behavior naturally.

### The Log-Linear Return Approximation

Using the Campbell-Shiller (1988) log-linearization, the log equity return can be approximated as:

$$
r^{eq}_{t+1} \approx \kappa_0 + \kappa_1 z_{t+1} - z_t + \Delta d_{t+1}
$$

where $\kappa_0$ and $\kappa_1$ are linearization constants (with $\kappa_1 \approx 0.997$ for an annual calibration with a reasonable price-dividend ratio). Substituting the expressions for $z_t$, $z_{t+1}$, and $\Delta d_{t+1}$:

$$
r^{eq}_{t+1} - \mathbb{E}_t[r^{eq}_{t+1}] = (\phi + \kappa_1 A_1 \varphi_e) \sigma_t e_{t+1} + (1 + \kappa_1 A_1) \sigma_t \eta_{t+1} + \varphi_d \sigma_t u_{t+1} + \kappa_1 A_2 \sigma_w w_{t+1}
$$

This expression decomposes unexpected equity returns into four components:

- **Long-run growth news** (loading on $e_{t+1}$): Shocks to expected growth $x_{t+1}$ are amplified by $\kappa_1 A_1$ because they change the price-dividend ratio, in addition to their direct effect on dividends through $\phi$.
- **Short-run consumption news** (loading on $\eta_{t+1}$): Current consumption shocks affect current dividends and feed into prices through the price-dividend ratio.
- **Idiosyncratic dividend news** (loading on $u_{t+1}$): Firm-specific shocks affect dividends but not the price-dividend ratio.
- **Volatility news** (loading on $w_{t+1}$): Shocks to the volatility state change the discount rate and therefore the price-dividend ratio through $A_2$.

The first and last components — long-run growth news and volatility news — are the distinctively Bansal-Yaron risks. They are small in magnitude (because $\varphi_e$ and $\sigma_w$ are calibrated to be small) but highly priced under Epstein-Zin preferences, because the SDF responds strongly to them.

### The Equity Premium

The equity premium in the model is:

$$
\mathbb{E}_t[r^{eq}_{t+1}] - r_{f,t} + \frac{\sigma^2_{eq,t}}{2} = \underbrace{\gamma \sigma^2_t (1 + \kappa_1 A_1)}_{\text{Short-run risk}} + \underbrace{\gamma \sigma^2_t \kappa_1 A_1 \phi \varphi_e^2}_{\text{Long-run growth risk}} + \underbrace{\lambda_\sigma \kappa_1 A_2 \sigma_w}_{\text{Volatility risk}}
$$

where $\lambda_\sigma = (\theta - 1)\sigma_w/(A_2)$ is the market price of volatility risk. Several features of this expression deserve emphasis:

**Time variation**: The equity premium depends on $\sigma^2_t$ through the first two terms. In periods of high volatility, the premium is higher — as it should be, since the risks are larger. This generates **countercyclical risk premia**: during recessions, volatility tends to rise, which mechanically raises the equity premium. This is consistent with the empirical evidence and is a prediction shared with the habit formation model, though the mechanism is entirely different.

**The long-run growth risk term** is amplified by $\kappa_1 A_1 \phi \varphi_e^2$. The factor $\kappa_1 A_1$ is large because $A_1$ is large — the price-dividend ratio is highly sensitive to expected growth under high-EIS preferences. A small shock to expected growth today cascades into a large revision in the price-dividend ratio, making equity highly exposed to $x_t$ shocks even though those shocks are individually tiny. This is the core amplification mechanism of the model.

**The volatility risk term** is proportional to $A_2 \sigma_w$ — the sensitivity of the price-dividend ratio to volatility times the volatility of volatility. When $A_2$ is large in absolute value (high uncertainty aversion) and $\sigma_w$ is non-negligible, volatility risk contributes substantially to the premium.

---

## 3. The Calibration and Its Mechanisms

### Parameter Values

Bansal and Yaron (2004) calibrate their model at a monthly frequency and then aggregate to annual moments. Their key parameters, expressed at an annual frequency for interpretability, are:

| Parameter | Value | Description |
|:---|---:|:---|
| $\mu_c$ | 1.80% | Mean consumption growth |
| $\bar{\sigma}$ | 1.50% | Unconditional consumption volatility |
| $\rho$ | 0.979 | Persistence of long-run risk $x_t$ |
| $\varphi_e$ | 0.044 | Volatility of long-run risk shocks |
| $\nu_1$ | 0.987 | Persistence of volatility |
| $\phi$ | 3.0 | Dividend leverage |
| $\gamma$ | 10.0 | Coefficient of relative risk aversion |
| $\psi$ | 1.5 | Elasticity of intertemporal substitution |
| $\beta$ | 0.998 | Discount factor |

Several features of this calibration deserve attention.

The long-run risk component $x_t$ has unconditional standard deviation $\varphi_e \bar{\sigma}/\sqrt{1-\rho^2} \approx 0.044 \times 0.015/\sqrt{1-0.979^2} \approx 0.22\%$ — tiny relative to the unconditional standard deviation of consumption growth of $1.5\%$. The signal-to-noise ratio is less than $15\%$. This is by design: the long-run risk component is deliberately calibrated to be nearly undetectable in short samples. Any researcher testing for predictability in consumption growth with 50 or 100 years of data would have very low power against this alternative. This is both the model's strength — the mechanism does not contradict observed data — and its weakness — the key ingredient is econometrically elusive.

The persistence $\rho = 0.979$ at annual frequency implies a half-life of approximately 33 years for shocks to expected growth. This is very slow mean reversion. An agent who learns today that expected growth has fallen from $1.8\%$ to $1.5\%$ per annum understands that this shortfall will persist for decades — a $0.3\%$ annual shortfall compounding over 33 years amounts to approximately a $10\%$ permanent reduction in the level of consumption. Under high EIS and high $\gamma$, this is priced as a very large risk.

### Why Small Shocks Have Large Price Effects

The amplification mechanism is best understood through the relationship between the price-dividend ratio and expected growth. Under Epstein-Zin preferences with $\psi > 1$, the present-value coefficient $A_1$ satisfies:

$$
A_1 = \frac{\kappa_1 \phi}{1 - \kappa_1 \rho}
$$

With $\kappa_1 \approx 0.997$ and $\rho = 0.979$: $A_1 = 0.997 \times 3/(1 - 0.997 \times 0.979) \approx 2.99/0.021 \approx 142$.

The price-dividend ratio has an elasticity of approximately $142$ with respect to $x_t$. A one-standard-deviation shock to expected growth of $0.22\%$ therefore changes the log price-dividend ratio by $142 \times 0.22\% \approx 31\%$ — a dramatic price movement from a tiny fundamental shock. This is the long-run risk model's central mechanism: the sensitivity of the price-dividend ratio to expected growth is enormous under high EIS, because the agent discounts the long-run consequences of the shock at a low rate.

Intuitively, when $\psi > 1$, the income effect of higher expected returns dominates the substitution effect — the agent wants to *increase* current consumption when future returns are expected to be higher. This creates a strong feedback: higher expected growth raises prices, which raises current wealth, which validates the higher consumption. The resulting price-dividend elasticity is amplified relative to the $\psi < 1$ case, where the substitution effect dominates and the agent *reduces* current consumption in response to higher expected future returns.

### Matched Moments

The Bansal-Yaron calibration matches the following annual moments:

| Moment | Data | Model |
|:---|---:|---:|
| Mean equity premium | 6.33% | 6.84% |
| Std. dev. of equity returns | 19.42% | 19.10% |
| Mean risk-free rate | 0.86% | 1.39% |
| Std. dev. of risk-free rate | 0.97% | 0.47% |
| Mean price-dividend ratio | 22.14 | 22.78 |
| Std. dev. of price-dividend ratio | 3.20 | 3.11 |

The match on the first four moments is close but not perfect — the model slightly overestimates the risk-free rate and underestimates its volatility. The match on the price-dividend ratio moments is excellent, which reflects the model's explicit mechanism for generating time-varying discount rates and hence volatile prices.

Importantly, the model achieves all of these with $\gamma = 10$ and $\psi = 1.5$ — parameters that are extreme by the standards of the earlier literature but far more modest than the $\gamma \geq 50$ required by the standard CRRA model. The long-run risk mechanism acts as a leverage device, amplifying the impact of a moderate $\gamma$ into large observable risk premia.

---

## 4. Return Predictability and the Price-Dividend Ratio

One of the most compelling features of the Bansal-Yaron model is its ability to generate return predictability quantitatively consistent with the data.

### Predictability from the Price-Dividend Ratio

Since the price-dividend ratio $z_t = A_0 + A_1 x_t + A_2 \sigma^2_t$ is a function of the state variables, and since these state variables are persistent, $z_t$ should forecast future returns. Specifically, when $z_t$ is low — when expected growth is low or uncertainty is high — expected returns are high. This generates the well-documented negative predictability of returns from the dividend yield (which is inversely related to $z_t$).

The model's implied predictability coefficient in a regression of long-horizon excess returns on the log price-dividend ratio is:

$$
b_h = \frac{\text{Cov}\left(\sum_{j=1}^h r^{eq}_{t+j}, z_t\right)}{\text{Var}(z_t)}
$$

Under the long-run risk model, $b_h$ is negative (lower prices predict higher future returns), increases in absolute value with the horizon $h$, and eventually flattens out at long horizons as the predictable component of returns is exhausted. This pattern is broadly consistent with the empirical evidence of Fama and French (1988) and Campbell and Shiller (1988), who found significant predictability of 3–5 year excess returns from the dividend yield, with the $R^2$ rising from about $3\%$ at one year to $25\%$ or more at three to five years.

The key mechanism is the interaction between the persistence of $x_t$ and the sensitivity of prices to $x_t$. Because $x_t$ is highly persistent, a period of low expected growth (low $z_t$) implies that the low expected growth will persist for many years, generating cumulatively high required returns. The cumulative predictability therefore increases with horizon, consistent with the data.

### Return Volatility and the Variance-Ratio Puzzle

A related implication is that the model generates **excess return volatility** relative to a model with constant expected returns. Under the long-run risk model, price changes reflect both cash flow news (shocks to current and expected dividends) and discount rate news (shocks to $x_t$ and $\sigma^2_t$). The variance of returns is therefore:

$$
\text{Var}(r^{eq}_{t+1}) = \text{Var}(\text{cash flow news}) + \text{Var}(\text{discount rate news}) + 2\text{Cov}(\ldots)
$$

The discount rate news component — driven by the volatility of $z_t$ — is substantial and accounts for a large share of total return variance. Campbell and Shiller (1988) showed empirically that most of the variance of stock returns comes from discount rate variation rather than cash flow variation — a finding that the long-run risk model naturally accommodates.

---

## 5. The Role of Stochastic Volatility

The second long-run risk component — time-varying consumption volatility $\sigma^2_t$ — is sometimes treated as secondary to the expected growth component, but it plays a crucial and distinct role.

### The Variance Premium

The **variance risk premium** (VRP) is the difference between risk-neutral variance (as measured by the VIX) and physical variance (as measured by realized variance):

$$
VRP_t = \mathbb{E}^{\mathbb{Q}}_t[\sigma^2_{t+1}] - \mathbb{E}_t[\sigma^2_{t+1}]
$$

Under the long-run risk model with stochastic volatility, the VRP is:

$$
VRP_t = -\lambda_\sigma \sigma_w = (\theta-1) \frac{\sigma_w^2}{A_2}
$$

where the sign follows from $A_2 < 0$ and $\theta > 1$ (when $\gamma > 1/\psi$). Periods of high realized volatility $\sigma^2_t$ are associated with high risk premia on variance-contingent claims — the market prices volatility risk positively.

This prediction is strongly supported empirically. Carr and Wu (2009) documented a large and persistent variance risk premium in equity options markets. Bollerslev, Tauchen, and Zhou (2009) showed that the VRP forecasts equity returns at quarterly horizons with high statistical power — an additional predictability result that the long-run risk model captures but that habit formation models miss, since they have no stochastic volatility component.

### Countercyclical Risk Premia Through Two Channels

With stochastic volatility, the equity premium is time-varying through two channels that are partly distinct:

**The volatility level channel**: When $\sigma^2_t$ is high, all risk premia based on quantity-of-risk measures rise, since the variance of all shocks is larger. The risk compensation for any given shock $e_{t+1}$, $\eta_{t+1}$, or $u_{t+1}$ rises proportionally with $\sigma^2_t$.

**The volatility uncertainty channel**: Shocks to $\sigma^2_t$ itself (the $w_{t+1}$ term) represent uncertainty about uncertainty — second-order risk. Under Epstein-Zin preferences with $\gamma > 1/\psi$, the agent dislikes increases in uncertainty about future welfare and prices this separately.

The first channel is present in any model with time-varying volatility. The second channel is specific to long-run risk models with stochastic volatility and Epstein-Zin preferences. Together, they make the model's implied Sharpe ratio strongly countercyclical, consistent with the empirical evidence from both options markets and time-series return regressions.

---

## 6. Empirical Challenges

Despite its remarkable quantitative success on many dimensions, the long-run risk model faces several empirical challenges that have generated a large critical literature.

### The Weak Evidence for Long-Run Predictability in Consumption

The model's central ingredient — the highly persistent predictable component $x_t$ in consumption growth — is nearly undetectable in available data. Beeler and Campbell (2012) showed through careful Monte Carlo analysis that:

- The model implies a return predictability pattern that is too strong relative to postwar data: the price-dividend ratio predicts returns at short horizons too powerfully.
- The model implies that dividend growth should be predictable from the price-dividend ratio — a prediction strongly at odds with the data, where the dividend yield predicts returns but not dividend growth.
- The correlation between consumption growth and stock returns implied by the model is substantially higher than observed — a version of the original equity premium puzzle that the model has not fully escaped.

The last point is particularly important. The model essentially solves the equity premium puzzle by making the SDF highly sensitive to the small $x_t$ component of consumption growth. But since $x_t$ is embedded in observed consumption growth along with much larger i.i.d. noise, the correlation between equity returns and observable consumption growth remains low — close to what the original Mehra-Prescott model implied. The long-run risk model has shifted the source of the puzzle from "why is the premium so large?" to "why is the correlation between consumption and returns so low?" — arguably without fully resolving either.

### The Peso Problem

The near-unit-root in $x_t$ ($\rho = 0.979$ annually) creates a subtle statistical problem: in any finite sample, the realized dynamics of $x_t$ will look approximately i.i.d. because the persistence is too slow to identify in 100–150 years of data. Researchers testing for predictability in consumption growth will routinely fail to detect the $x_t$ component and will correctly conclude (based on their sample) that consumption growth is approximately i.i.d. The model is calibrated to a true data-generating process that has different low-frequency properties from what any finite sample would reveal — a version of the peso problem. This makes the model empirically unfalsifiable in a deep sense: any short-run evidence against it can always be attributed to the econometrician's inability to identify the long-run component.

### The Joint Behavior of Consumption and Dividends

The dividend leverage parameter $\phi = 3$ is needed to match the volatility of equity returns — dividends must be riskier than consumption. But this creates a tension: with $\phi = 3$, the model predicts that dividend growth is highly predictable from $x_t$ and therefore from the price-dividend ratio. In practice, dividend growth shows little or no predictability from the price-dividend ratio. This dividend predictability failure is one of the model's most cited empirical shortcomings.

Larrain and Yogo (2008) and Beeler and Campbell (2012) both document this problem carefully. It has motivated extensions of the model that introduce additional idiosyncratic dividend volatility to reduce spurious dividend predictability — but at the cost of adding parameters and weakening the theoretical elegance of the calibration.

### The High $\psi$ Requirement

The model requires $\psi > 1$ for the amplification mechanism to work. As discussed in Block 3.3, aggregate consumption data tends to yield EIS estimates close to zero or at most $0.5$ using standard regression approaches. The structural estimates of Bansal, Kiku, and Yaron (2012) that recover $\psi \approx 1.5$ rely on the model being correctly specified — a circularity that critics have noted. The high-EIS requirement remains one of the most contested aspects of the long-run risk framework.

---

## 7. Extensions and the Long-Run Risk Literature

The original Bansal-Yaron (2004) model spawned an extensive literature of extensions addressing its limitations and exploring new implications.

### Bansal, Kiku, and Yaron (2012): Structural Estimation

Rather than calibration, Bansal, Kiku, and Yaron (2012) estimated the model structurally using GMM, allowing all parameters to be identified jointly from both consumption and return data. Their estimates confirm the high $\psi$ and moderate $\gamma$ of the calibration and provide standard errors for the key parameters. The structural approach also allows formal testing of the model against alternatives — something that pure calibration does not permit.

### Drechsler and Yaron (2011): Uncertainty and the Variance Premium

Drechsler and Yaron (2011) extended the model to match the dynamics of the VIX and the variance risk premium. Their model features jumps in consumption growth and volatility, generating a richer distribution of outcomes that better matches the fat tails of return distributions and the large observed VRP. The extension confirms that stochastic volatility is not merely an empirical convenience but a conceptually important source of risk with distinct pricing implications.

### Bansal and Shaliastovich (2013): The Term Structure

Long-run risk models have natural implications for the term structure of interest rates. Bansal and Shaliastovich (2013) showed that the model generates an upward-sloping term structure of equity yields (as documented empirically by Binsbergen, Brandt, and Koijen, 2012) and a realistic term premium on nominal bonds once inflation uncertainty is incorporated. The key is that long-maturity bonds are exposed to long-run inflation and real growth risk — exactly the type of risk that is highly priced under Epstein-Zin preferences.

### Binsbergen and Koijen (2017): Dividend Claims and the Term Structure of Equity

Binsbergen, Brandt, and Koijen (2012) and Binsbergen and Koijen (2017) used market prices of short-maturity dividend claims (synthetic assets paying dividends over the next 1–5 years) to directly test the term structure of equity risk premia. Their finding that short-maturity dividend claims earn *higher* expected returns than the aggregate market is a challenge for the standard long-run risk model, which implies the opposite: short-horizon cash flows are less exposed to long-run risk than the aggregate and should have lower expected returns. This "short-maturity equity premium" puzzle has generated active theoretical and empirical work, with various explanations including liquidity premia, dividend seasonality, and model misspecification.

---

## 8. Long-Run Risk vs. Habit Formation: A Synthesis

Having now developed both the habit formation and long-run risk frameworks in depth, it is instructive to compare them systematically against the criteria established in Block 3.1.

| Criterion | Habit Formation (CC) | Long-Run Risk (BY) |
|:---|:---|:---|
| Equity premium | ✓ Matched by construction | ✓ Matched by calibration |
| Risk-free rate level | ✓ Matched by construction | ✓ Approximately matched |
| Risk-free rate volatility | ✗ Zero by assumption | ✗ Too low |
| Return volatility | ✓ Matched | ✓ Matched |
| Return predictability | ✓ From dividend yield | ✓ From dividend yield |
| Variance risk premium | ✗ No stochastic volatility | ✓ Generated naturally |
| Plausible EIS | ✓ $\psi = 0.5$ | ✗ Requires $\psi > 1$ |
| Plausible $\gamma$ | ✓ $\gamma = 2$ (effective $\gamma/S$) | ~ $\gamma = 10$ |
| Consumption predictability | ✓ Not required | ✗ Required but barely detectable |
| Dividend predictability | Neutral | ✗ Overpredicted |

Neither model dominates on all criteria. Habit formation achieves its results with more modest assumptions about the EIS and generates a richer theory of state-dependent risk aversion, but requires the economy to perpetually hover near the subsistence boundary and cannot address volatility risk pricing. Long-run risk provides a natural theory of the variance premium, generates rich term structure implications, and resolves the EIS-RRA tension — but requires a highly persistent consumption process component that is essentially undetectable in historical data and generates too much dividend predictability.

The most productive view is to treat the two frameworks as complements rather than substitutes: habit formation captures the backward-looking amplification of risk aversion during periods of declining consumption, while long-run risk captures the forward-looking sensitivity to persistent changes in growth prospects. A unified model incorporating both mechanisms would likely outperform either in isolation — and indeed, several papers have moved in this direction.

---

## Key Takeaways

**Long-run risk is the combination of a small but highly persistent predictable component in consumption growth ($x_t$) and time-varying consumption volatility ($\sigma^2_t$).** Neither component is easily detectable in short samples, but both generate large risk premia under Epstein-Zin preferences with high EIS.

**The amplification mechanism works through the price-dividend ratio.** Under high EIS, the price-dividend ratio is extremely sensitive to expected growth — a tiny shock to $x_t$ generates a large revision in stock prices because the agent extrapolates the persistent shock far into the future. This makes equity highly exposed to long-run growth risk even when the quantitative magnitude of $x_t$ is tiny.

**Stochastic volatility generates a distinct second source of risk.** Shocks to $\sigma^2_t$ — volatility of volatility — are priced separately under Epstein-Zin preferences, generating a positive variance risk premium consistent with options market data. This is a prediction that habit formation models cannot generate.

**The model matches an unusually broad set of moments.** Equity premium, risk-free rate, return volatility, price-dividend ratio volatility, return predictability, and the variance premium are all broadly consistent with the model's implications at $\gamma = 10$ and $\psi = 1.5$.

**Key empirical challenges remain.** The long-run risk component is nearly undetectable in historical data (raising identification concerns), dividend growth predictability is overpredicted, and the short-maturity equity premium puzzle runs counter to the model's term structure implications. The high EIS requirement is contested.

**Habit formation and long-run risk are best viewed as complementary frameworks** capturing distinct aspects of the SDF's dynamics — backward-looking state-dependent risk aversion and forward-looking sensitivity to persistent growth news, respectively.

---

## Looking Ahead: Block 3.5 — Rare Disasters

Blocks 3.2 through 3.4 developed two families of resolutions to the equity premium puzzle — habit formation and the recursive preference / long-run risk paradigm — both of which operate by making the SDF more volatile through relatively subtle modifications to preferences and the consumption process. Block 3.5 takes an entirely different approach. Barro (2006), building on Rietz (1988), argued that the equity premium can be rationalized by the *rare but catastrophic possibility of economic disasters* — events like the Great Depression, hyperinflations, or wars. Even if such disasters have a small probability in any given year, their contribution to the expected value of the SDF can be enormous if they are sufficiently severe and if agents are sufficiently risk-averse. The rare disaster model requires no modification to expected utility and no exotic consumption dynamics — it only requires taking seriously the full distribution of consumption outcomes, including the extreme left tail that normal-distribution calibrations discard.

---

*Block 3.3 — Recursive Preferences | **Block 3.4 — Long-Run Risk** | Block 3.5 — Rare Disasters →*
