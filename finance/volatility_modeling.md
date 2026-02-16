# Volatility Modeling

## The ARCH Family

The fundamental insight of Engle (1982) was that **volatility is time-varying and predictable from past squared residuals**. The ARCH(q) model specifies:

$$r_t = \mu + \varepsilon_t, \qquad \varepsilon_t = \sigma_t z_t, \quad z_t \overset{iid}{\sim} (0,1)$$

$$\sigma_t^2 = \omega + \sum_{i=1}^{q} \alpha_i \varepsilon_{t-i}^2$$

For covariance stationarity we require $\omega > 0$, $\alpha_i \geq 0$, and $\sum \alpha_i < 1$.

## GARCH(1,1)

Bollerslev (1986) extended ARCH to include lagged conditional variance terms, yielding the **GARCH(p,q)** model. The canonical GARCH(1,1) is:

$$\sigma_t^2 = \omega + \alpha \varepsilon_{t-1}^2 + \beta \sigma_{t-1}^2$$

The **persistence** of volatility shocks is measured by $\alpha + \beta$. In practice, estimates near financial data give $\alpha + \beta \approx 0.97$–$0.99$, implying **highly persistent** but mean-reverting volatility.

```{note}
The unconditional variance under GARCH(1,1) is $\bar{\sigma}^2 = \frac{\omega}{1 - \alpha - \beta}$, provided $\alpha + \beta < 1$.
```

## Asymmetric Extensions

Standard GARCH is symmetric — it treats positive and negative shocks identically. Empirically, negative shocks tend to increase volatility more than positive shocks of the same magnitude. This is the **leverage effect**.

**GJR-GARCH (Glosten, Jagannathan, Runkle, 1993):**

$$\sigma_t^2 = \omega + \alpha \varepsilon_{t-1}^2 + \gamma \varepsilon_{t-1}^2 \mathbf{1}[\varepsilon_{t-1} < 0] + \beta \sigma_{t-1}^2$$

Here $\gamma > 0$ captures the asymmetry: bad news contributes $\alpha + \gamma$ to next period's variance, good news only $\alpha$.

**EGARCH (Nelson, 1991):**

$$\ln \sigma_t^2 = \omega + \alpha \left(\frac{|\varepsilon_{t-1}|}{\sigma_{t-1}} - \sqrt{2/\pi}\right) + \gamma \frac{\varepsilon_{t-1}}{\sigma_{t-1}} + \beta \ln \sigma_{t-1}^2$$

EGARCH models the **log-variance**, which automatically ensures positivity without parameter constraints.

## Model Comparison

| Model | Asymmetry | Positivity Constraint | Parameters |
|-------|-----------|----------------------|------------|
| GARCH(1,1) | ✗ | $\omega, \alpha, \beta > 0$ | 3 |
| GJR-GARCH | ✓ | $\omega, \alpha, \beta \geq 0$; $\alpha + \gamma \geq 0$ | 4 |
| EGARCH(1,1) | ✓ | None (log specification) | 4 |

## Estimation in Python

```python
import pandas as pd
import yfinance as yf
from arch import arch_model

# Download data
ticker = yf.Ticker("^GSPC")
prices  = ticker.history(start="2015-01-01", end="2024-01-01")["Close"]
returns = 100 * prices.pct_change().dropna()

# GARCH(1,1) with normal errors
garch  = arch_model(returns, vol="Garch", p=1, q=1, dist="normal")
result = garch.fit(disp="off")
print(result.summary())

# GJR-GARCH with Student-t errors
gjr    = arch_model(returns, vol="Garch", p=1, o=1, q=1, dist="t")
result_gjr = gjr.fit(disp="off")
print(result_gjr.summary())
```

## References

- Engle, R. F. (1982). Autoregressive conditional heteroscedasticity with estimates of the variance of United Kingdom inflation. *Econometrica*, 50(4), 987–1007.
- Bollerslev, T. (1986). Generalized autoregressive conditional heteroskedasticity. *Journal of Econometrics*, 31(3), 307–327.
- Nelson, D. B. (1991). Conditional heteroskedasticity in asset returns: A new approach. *Econometrica*, 59(2), 347–370.
