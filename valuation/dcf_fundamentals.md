# DCF Fundamentals

## The Core Principle

The **Discounted Cash Flow (DCF)** model values a firm (or project) as the present value of its expected future free cash flows:

$$V_0 = \sum_{t=1}^{T} \frac{FCFF_t}{(1+WACC)^t} + \frac{TV_T}{(1+WACC)^T}$$

where $FCFF_t$ is the Free Cash Flow to the Firm in period $t$, $WACC$ is the Weighted Average Cost of Capital, and $TV_T$ is the **terminal value** — the value of all cash flows beyond the explicit forecast horizon.

## Free Cash Flow to the Firm

$$FCFF = EBIT(1 - \tau) + D\&A - \Delta NWC - CAPEX$$

| Component | Description |
|-----------|-------------|
| $EBIT(1-\tau)$ | NOPAT — operating profit after tax |
| $+D\&A$ | Non-cash charge added back |
| $-\Delta NWC$ | Investment in net working capital |
| $-CAPEX$ | Capital expenditures (growth and maintenance) |

```{note}
FCFF is the cash available to **all capital providers** (debt and equity). It should be discounted at the WACC, not the cost of equity. Discounting FCFF at the cost of equity is a common error.
```

## The Weighted Average Cost of Capital

$$WACC = \frac{E}{V} \cdot r_e + \frac{D}{V} \cdot r_d \cdot (1 - \tau)$$

where $E/(E+D)$ and $D/(E+D)$ are the **target** (not current) capital structure weights at market value, $r_e$ is the cost of equity, $r_d$ the pre-tax cost of debt, and $\tau$ the marginal tax rate.

### Cost of Equity — CAPM

$$r_e = r_f + \beta \cdot (r_m - r_f)$$

The equity beta $\beta$ measures the firm's sensitivity to market risk. It should be estimated from comparable firms, unlevered, and re-levered to the target capital structure (Hamada equation):

$$\beta_L = \beta_U \left[1 + (1-\tau)\frac{D}{E}\right]$$

## Terminal Value

The terminal value typically represents 60–80% of the total DCF value — making it the most sensitive and most debated component.

**Gordon Growth Model (perpetuity growth):**

$$TV_T = \frac{FCFF_{T+1}}{WACC - g} = \frac{FCFF_T(1+g)}{WACC - g}$$

The long-run growth rate $g$ should not exceed the long-run nominal GDP growth rate — any higher and the firm eventually becomes the entire economy.

**Exit multiple method:**

$$TV_T = EBITDA_T \times \text{Exit Multiple}$$

Anchoring to a market multiple introduces circular reasoning (the multiple itself reflects DCF-based market prices) but provides a useful sanity check.

## Python: A Simple DCF Model

```python
import numpy as np

def dcf_valuation(fcff_base, growth_rates, terminal_growth, wacc, net_debt, shares):
    """
    Simple DCF valuation.

    Parameters
    ----------
    fcff_base      : float  — Current year FCFF (year 0)
    growth_rates   : list   — Explicit forecast period growth rates (one per year)
    terminal_growth: float  — Perpetuity growth rate after explicit period
    wacc           : float  — Discount rate
    net_debt       : float  — Net debt (Enterprise Value → Equity Value bridge)
    shares         : float  — Shares outstanding

    Returns
    -------
    dict with enterprise value, equity value, intrinsic price per share
    """
    # Explicit forecast period
    fcff = fcff_base
    pv_fcff = 0.0
    for t, g in enumerate(growth_rates, start=1):
        fcff *= (1 + g)
        pv_fcff += fcff / (1 + wacc) ** t

    # Terminal value
    T = len(growth_rates)
    tv = fcff * (1 + terminal_growth) / (wacc - terminal_growth)
    pv_tv = tv / (1 + wacc) ** T

    enterprise_value = pv_fcff + pv_tv
    equity_value     = enterprise_value - net_debt
    price_per_share  = equity_value / shares

    return {
        "PV of explicit FCFFs": round(pv_fcff, 1),
        "PV of Terminal Value": round(pv_tv, 1),
        "Enterprise Value":     round(enterprise_value, 1),
        "Equity Value":         round(equity_value, 1),
        "Intrinsic Price":      round(price_per_share, 2),
        "TV % of EV":           round(100 * pv_tv / enterprise_value, 1),
    }


# Example: hypothetical industrial company
result = dcf_valuation(
    fcff_base       = 500,           # €500m FCFF
    growth_rates    = [0.10, 0.09, 0.08, 0.07, 0.06],  # 5-year explicit period
    terminal_growth = 0.025,         # 2.5% perpetuity growth
    wacc            = 0.09,          # 9% WACC
    net_debt        = 800,           # €800m net debt
    shares          = 200            # 200m shares
)

for k, v in result.items():
    print(f"  {k:30s}: {v}")
```

## Sensitivity Analysis

DCF outputs are highly sensitive to assumptions. A proper valuation always includes a **sensitivity table** showing how the intrinsic price varies with WACC and the terminal growth rate.

```python
import pandas as pd

wacc_range = [0.07, 0.08, 0.09, 0.10, 0.11]
tg_range   = [0.015, 0.020, 0.025, 0.030, 0.035]

table = pd.DataFrame(index=[f"g={g:.1%}" for g in tg_range],
                     columns=[f"WACC={w:.1%}" for w in wacc_range])

for g in tg_range:
    for w in wacc_range:
        res = dcf_valuation(
            fcff_base=500, growth_rates=[0.10, 0.09, 0.08, 0.07, 0.06],
            terminal_growth=g, wacc=w, net_debt=800, shares=200
        )
        table.loc[f"g={g:.1%}", f"WACC={w:.1%}"] = f"€{res['Intrinsic Price']}"

print(table.to_string())
```

## References

- Damodaran, A. (2012). *Investment Valuation* (3rd ed.). Wiley Finance.
- Koller, T., Goedhart, M., & Wessels, D. (2020). *Valuation: Measuring and Managing the Value of Companies* (7th ed.). McKinsey & Company / Wiley.
