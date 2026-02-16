# Multiples and Comparables

## Why Multiples?

Relative valuation anchors value to **market prices of comparable firms**. Instead of forecasting cash flows explicitly, we ask: *"What are investors paying for similar businesses right now?"*

Multiples are:
- **Fast** — no multi-year forecast required
- **Market-anchored** — reflects current sentiment and pricing
- **Intuitive** — easy to communicate to non-specialists

But they are also:
- **Circular** — if markets are wrong, multiples inherit that error
- **Comparability-sensitive** — garbage in, garbage out if peers are chosen poorly
- **Accounting-sensitive** — different depreciation policies distort earnings-based multiples

## Enterprise Value vs Equity Value Multiples

| Multiple | Numerator | Denominator | Who bears it? |
|----------|-----------|-------------|---------------|
| EV/EBITDA | Enterprise Value | EBITDA | All capital providers |
| EV/EBIT | Enterprise Value | EBIT | All capital providers |
| EV/Sales | Enterprise Value | Revenue | All capital providers |
| P/E | Market Cap | Net Income | Equity holders only |
| P/B | Market Cap | Book Equity | Equity holders only |

```{important}
Always match numerator to denominator: **EV multiples** use pre-debt income metrics (EBITDA, EBIT, Sales). **Equity multiples** use post-debt metrics (Net Income, Book Equity). Mixing them is a fundamental error.
```

## EV/EBITDA: The Practitioner's Workhorse

EV/EBITDA is preferred because:
- It is **capital structure-neutral** (before interest)
- It is less affected by depreciation policy differences than EV/EBIT
- It is **positive** for most profitable firms (P/E can be negative for loss-making firms)

Typical EV/EBITDA ranges by sector (2020s, approximate):

| Sector | Typical Range |
|--------|--------------|
| Technology / Software | 15–30× |
| Healthcare | 12–20× |
| Consumer Staples | 10–15× |
| Industrials | 8–12× |
| Utilities | 7–10× |
| Energy | 4–8× |

These ranges shift significantly with interest rates and market cycles.

## Adjustments for Comparability

Raw multiples are misleading when peers differ in growth or risk. The **PEG ratio** adjusts P/E for growth:

$$PEG = \frac{P/E}{g}$$

where $g$ is the expected EPS growth rate (%). A PEG of 1 is often used as a heuristic for fair value.

For EV multiples, a regression-based approach regresses the multiple on fundamentals across the peer group:

$$\frac{EV_i}{EBITDA_i} = \alpha + \beta_1 g_i + \beta_2 \text{ROIC}_i + \beta_3 \text{Leverage}_i + \varepsilon_i$$

The fitted value for the target firm becomes the "warranted" multiple.

## Python: Comparable Company Analysis

```python
import pandas as pd
import numpy as np

# Hypothetical peer group data
peers = pd.DataFrame({
    "Company":       ["Alpha Co", "Beta Corp", "Gamma Inc", "Delta Ltd", "Epsilon SA"],
    "EV_m":          [4200, 2800, 6100, 1500, 3300],     # Enterprise value €m
    "EBITDA_m":      [380,  210,  490,  140,  280],       # EBITDA €m
    "Revenue_m":     [1200, 850,  1600, 500,  950],       # Revenue €m
    "EBIT_margin":   [0.18, 0.15, 0.19, 0.17, 0.18],     # EBIT / Revenue
    "Growth_3y":     [0.08, 0.12, 0.07, 0.15, 0.09],     # Revenue CAGR
})

peers["EV_EBITDA"] = peers["EV_m"] / peers["EBITDA_m"]
peers["EV_Revenue"] = peers["EV_m"] / peers["Revenue_m"]

print("=== Peer Group Multiples ===")
cols = ["Company", "EV_EBITDA", "EV_Revenue", "EBIT_margin", "Growth_3y"]
print(peers[cols].to_string(index=False, float_format="{:.2f}".format))

# Summary statistics
print("\n=== Multiple Summary ===")
print(peers[["EV_EBITDA", "EV_Revenue"]].describe().round(2))

# Apply to target company
target_ebitda   = 320  # €m
target_revenue  = 1050 # €m

median_ev_ebitda  = peers["EV_EBITDA"].median()
median_ev_revenue = peers["EV_Revenue"].median()

ev_from_ebitda  = median_ev_ebitda  * target_ebitda
ev_from_revenue = median_ev_revenue * target_revenue

print(f"\n=== Target Valuation ===")
print(f"  EV/EBITDA method: €{ev_from_ebitda:.0f}m  (median {median_ev_ebitda:.1f}x × €{target_ebitda}m EBITDA)")
print(f"  EV/Revenue method: €{ev_from_revenue:.0f}m (median {median_ev_revenue:.2f}x × €{target_revenue}m revenue)")
print(f"  Implied range: €{min(ev_from_ebitda, ev_from_revenue):.0f}m – €{max(ev_from_ebitda, ev_from_revenue):.0f}m")
```

## Pitfalls and Best Practices

**Peer selection** is the most important and most subjective step. Peers should be similar in business model, geography, size, and growth profile. Including a high-growth tech firm in a peer group of mature industrials will distort every multiple.

**Trailing vs forward multiples**: Forward multiples (based on consensus earnings forecasts) are more appropriate for valuation because they reflect the future. Trailing multiples mix past performance with current prices.

**LTM vs FY multiples**: Use the last twelve months (LTM) figure to get the most current snapshot, especially when there are seasonal effects or recent acquisitions.
