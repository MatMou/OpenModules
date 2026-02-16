# Distributions and Statistical Inference

## Key Distributions in Finance

### The Normal Distribution

The normal distribution $\mathcal{N}(\mu, \sigma^2)$ has density:

$$f(x) = \frac{1}{\sigma\sqrt{2\pi}} \exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right)$$

Despite its theoretical elegance, it is a **poor model for financial returns** due to the stylized facts (fat tails, skewness). However, it remains useful as a benchmark and for Central Limit Theorem arguments on aggregated returns.

### The Student-t Distribution

For modeling fat tails, the Student-t distribution with $\nu$ degrees of freedom is far more appropriate:

$$f(x) = \frac{\Gamma\left(\frac{\nu+1}{2}\right)}{\sqrt{\nu\pi}\,\Gamma\left(\frac{\nu}{2}\right)}\left(1+\frac{x^2}{\nu}\right)^{-\frac{\nu+1}{2}}$$

As $\nu \to \infty$, the t-distribution converges to the normal. For $\nu < 30$, the heavier tails are practically relevant. For daily equity returns, fitted $\nu$ values typically fall between 4 and 8.

```{important}
For $\nu \leq 4$, the kurtosis is infinite. This matters: many financial series exhibit such extreme tail behavior that moments beyond the variance may not exist.
```

### Skewed Distributions

Returns are often negatively skewed — the left tail (crashes) is heavier than the right. The **skewed-t distribution** (Hansen, 1994) introduces an asymmetry parameter $\lambda \in (-1, 1)$ to the Student-t, providing more flexibility for realistic return modeling.

## Hypothesis Testing Framework

### The Logic of Testing

A hypothesis test proceeds as follows:

1. State the **null hypothesis** $H_0$ and alternative $H_1$
2. Choose a **test statistic** $T$ whose distribution under $H_0$ is known
3. Compute the **p-value**: $p = P(|T| \geq |t_{\text{obs}}| \mid H_0)$
4. **Reject $H_0$** if $p < \alpha$ (significance level, typically 5%)

### Tests for Normality

**Jarque-Bera test** — based on skewness ($\hat{S}$) and excess kurtosis ($\hat{K}$):

$$JB = \frac{n}{6}\left(\hat{S}^2 + \frac{\hat{K}^2}{4}\right) \overset{H_0}{\sim} \chi^2(2)$$

The JB test is very powerful for large samples, making it almost always reject normality for financial data — which is the correct conclusion. It is less useful for small samples.

**Shapiro-Wilk test** — generally preferred for smaller samples ($n < 2000$). Computes the correlation between the ordered sample and expected normal order statistics.

## Practical Example

```python
import numpy as np
import pandas as pd
from scipy import stats
import matplotlib.pyplot as plt

np.random.seed(0)
n = 500

# Simulate: normal returns vs t-distributed returns
r_normal = np.random.normal(0, 0.01, n)
r_t      = stats.t.rvs(df=5, scale=0.01, size=n)

for label, r in [("Normal", r_normal), ("t(5)", r_t)]:
    jb_stat, jb_pval = stats.jarque_bera(r)
    sw_stat, sw_pval = stats.shapiro(r[:200])   # Shapiro-Wilk on subsample
    kurt = stats.kurtosis(r)
    skew = stats.skew(r)
    print(f"\n{label}:")
    print(f"  Skewness: {skew:.3f}, Excess Kurtosis: {kurt:.3f}")
    print(f"  Jarque-Bera: stat={jb_stat:.2f}, p={jb_pval:.4f}")
    print(f"  Shapiro-Wilk (n=200): stat={sw_stat:.4f}, p={sw_pval:.4f}")
```

## Common Pitfalls

**P-hacking**: Running many tests and reporting only the significant ones inflates the false positive rate. If you run 20 independent tests at the 5% level, you expect 1 spurious rejection even if all nulls are true.

**Multiple testing corrections**: The Bonferroni correction adjusts the threshold to $\alpha/m$ for $m$ simultaneous tests. More powerful alternatives include the Benjamini-Hochberg procedure (controls the false discovery rate rather than the family-wise error rate).

**Economic vs statistical significance**: With large samples, trivially small effects become statistically significant. Always report effect sizes alongside p-values.
