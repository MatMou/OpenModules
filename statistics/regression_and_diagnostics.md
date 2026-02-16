# Regression and Diagnostics

## OLS in the Finance Context

Ordinary Least Squares (OLS) regression is the workhorse of empirical finance. Factor models, event studies, and predictive regressions are all built on it. The canonical setup:

$$r_t = \alpha + \beta_1 f_{1t} + \beta_2 f_{2t} + \cdots + \beta_k f_{kt} + \varepsilon_t$$

where $r_t$ is an asset's excess return and $f_{it}$ are factor returns (e.g., Fama-French factors).

## Gauss-Markov Assumptions

OLS is **BLUE** (Best Linear Unbiased Estimator) when:

1. **Linearity**: The model is linear in parameters
2. **No perfect multicollinearity**: Regressors are not perfectly linearly dependent
3. **Zero conditional mean**: $E[\varepsilon_t \mid X] = 0$
4. **Homoskedasticity**: $\text{Var}(\varepsilon_t \mid X) = \sigma^2$ (constant)
5. **No autocorrelation**: $\text{Cov}(\varepsilon_t, \varepsilon_s \mid X) = 0$ for $t \neq s$

Financial data routinely violates assumptions 4 and 5. Understanding when this matters (inference) vs. when it doesn't (point estimates) is essential.

## The Fama-French Three-Factor Model

The three-factor model (Fama & French, 1993) extends the CAPM with size (SMB) and value (HML) factors:

$$r_{it} - r_{ft} = \alpha_i + \beta_i^{MKT}(r_{mt} - r_{ft}) + \beta_i^{SMB} \cdot SMB_t + \beta_i^{HML} \cdot HML_t + \varepsilon_{it}$$

A non-zero $\alpha_i$ (Jensen's alpha) indicates abnormal risk-adjusted return — the central object of interest in performance evaluation.

## Key Diagnostic Tests

### Heteroskedasticity

When $\text{Var}(\varepsilon_t)$ is not constant, OLS standard errors are biased. The solution is **heteroskedasticity-robust standard errors** (White, 1980), which are now standard practice.

**White test**: Regress $\hat{\varepsilon}_t^2$ on all regressors, their squares, and cross-products. The test statistic $nR^2 \sim \chi^2(k)$.

**Breusch-Pagan test**: A simpler version assuming the variance is a linear function of the regressors.

### Autocorrelation

Time series residuals are often autocorrelated. The **Ljung-Box test** checks for autocorrelation up to lag $h$:

$$Q(h) = n(n+2)\sum_{k=1}^{h} \frac{\hat{\rho}_k^2}{n-k} \overset{H_0}{\sim} \chi^2(h)$$

For financial return regressions, the **Newey-West correction** adjusts standard errors for both heteroskedasticity and autocorrelation (HAC standard errors).

## Python Implementation

```python
import numpy as np
import pandas as pd
import statsmodels.api as sm
from statsmodels.stats.diagnostic import het_breuschpagan, acorr_ljungbox

np.random.seed(1)
n = 500

# Simulate a simple factor model
mkt  = np.random.normal(0.005, 0.02, n)
smb  = np.random.normal(0.002, 0.01, n)
eps  = np.random.normal(0, 0.01, n)
ret  = 0.001 + 0.8 * mkt + 0.3 * smb + eps   # true alpha = 0.001

X = sm.add_constant(np.column_stack([mkt, smb]))
model = sm.OLS(ret, X).fit()

# Standard errors comparison
print("=== Standard OLS SEs ===")
print(model.summary().tables[1])

model_hc = model.get_robustcov_results(cov_type='HC3')
print("\n=== Heteroskedasticity-Robust SEs (HC3) ===")
print(model_hc.summary().tables[1])

# Newey-West HAC standard errors
model_hac = model.get_robustcov_results(cov_type='HAC', maxlags=5)
print("\n=== Newey-West HAC SEs (5 lags) ===")
print(model_hac.summary().tables[1])

# Diagnostic tests
bp_stat, bp_pval, _, _ = het_breuschpagan(model.resid, X)
lb_result = acorr_ljungbox(model.resid, lags=[10], return_df=True)
print(f"\nBreusch-Pagan test: stat={bp_stat:.3f}, p={bp_pval:.4f}")
print(f"Ljung-Box test (10 lags): stat={lb_result['lb_stat'].values[0]:.3f}, "
      f"p={lb_result['lb_pvalue'].values[0]:.4f}")
```

## When to Use Which Standard Errors

| Situation | Recommended SE |
|-----------|---------------|
| i.i.d. errors (rare in finance) | OLS standard |
| Heteroskedasticity only | HC3 robust |
| Autocorrelation + heteroskedasticity | Newey-West HAC |
| Panel data, clustering | Clustered SE |

## References

- White, H. (1980). A heteroskedasticity-consistent covariance matrix estimator and a direct test for heteroskedasticity. *Econometrica*, 48(4), 817–838.
- Newey, W. K., & West, K. D. (1987). A simple, positive semi-definite, heteroskedasticity and autocorrelation consistent covariance matrix. *Econometrica*, 55(3), 703–708.
- Fama, E. F., & French, K. R. (1993). Common risk factors in the returns on stocks and bonds. *Journal of Financial Economics*, 33(1), 3–56.
