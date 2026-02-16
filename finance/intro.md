# Financial Econometrics

This module covers the core econometric tools used in empirical finance research and practice. The unifying theme is that **financial time series have distinctive statistical properties** — fat tails, volatility clustering, non-normality — that standard econometric tools were not designed for. We build the methods that respect these properties.

## Module Overview

```{list-table}
:header-rows: 1
:widths: 10 40 50

* - Week
  - Topic
  - Key Methods
* - 1–2
  - Returns and Stylized Facts
  - Log-returns, ACF/PACF, moment analysis
* - 3–5
  - Volatility Modeling
  - ARCH, GARCH, GJR-GARCH, EGARCH
* - 6–7
  - Multivariate Volatility
  - DCC-GARCH, BEKK
* - 8–9
  - Realized Volatility
  - Realized variance, HAR model
* - 10
  - Spillover Analysis
  - Diebold-Yilmaz connectedness
```

## Software

All code in this module uses Python. The main libraries are:

- `numpy`, `pandas` — data manipulation
- `arch` — GARCH estimation
- `statsmodels` — regression, ACF, diagnostics
- `matplotlib`, `seaborn` — visualization

You can install everything with:

```bash
pip install numpy pandas arch statsmodels matplotlib seaborn yfinance
```
