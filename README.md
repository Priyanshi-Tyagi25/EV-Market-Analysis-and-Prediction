# EV-Market-Analysis-and-Prediction
An end-to-end data science project analyzing global electric vehicle (EV) market growth, built as a portfolio piece: data prep → EDA → growth metrics
(YoY, CAGR) → forecasting (2026–2030) → regional breakdown → insights.

## Project Structure
```
ev_market_analysis/
├── data/
│   ├── ev_global_sales.csv       # Global EV sales & market share, 2015-2025
│   └── ev_regional_sales.csv     # Sales by region (China/Europe/US/RoW)
├── notebooks/
│   └── EV_Market_Growth_Analysis.ipynb   # Full analysis, fully executed with outputs
├── charts/                       # Standalone PNG exports of every chart
│   ├── 01_sales_and_share.png
│   ├── 02_regional_stacked.png
│   ├── 03_yoy_vs_cagr.png
│   ├── 04_forecast.png
│   └── 05_regional_mix_latest.png
└── README.md
```

## How to run
```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
cd notebooks
jupyter notebook EV_Market_Growth_Analysis.ipynb
```
The notebook is already executed and saved with outputs, so you can also just
open and read it without re-running anything.

## Methodology at a glance
- **Growth metrics:** YoY % growth (noisy, year-to-year) vs. CAGR (smoothed,
  headline comparison) — computed both for the full decade and by 5-year
  window to check whether growth is accelerating or maturing.
- **Forecasting:** two simple, transparent models compared side by side
  (log-linear on the full history vs. linear on the last 5 years only),
  rather than one black-box model fit to just 11 data points. The recent-
  trend model is favored because it better reflects the market's observed
  deceleration (S-curve behavior).
- **Regional analysis:** stacked-area trend + latest-year mix + per-region
  CAGR, to separate "who has the most volume" from "who is growing fastest."

## Data note
Global figures are anchored to publicly reported IEA *Global EV Outlook 2025*
aggregates (e.g., 17M+ global EV sales in 2024, >20% market share; ~20M+
projected for 2025). The regional split is a reasonable estimate built to
match those aggregates, since IEA's row-level regional data requires an
interactive account. Swap in a licensed IEA/EV-Volumes export to make this
production-ready — the pipeline itself doesn't change.

## Key findings
1. Global EV sales grew roughly **44x from 2015 to 2025** (~44% CAGR), but
   the *growth rate* is decelerating — a classic S-curve, not runaway
   exponential growth.
2. **Market penetration** (EV share of all new car sales) is a steadier
   growth signal than volume growth rate: it climbed from <1% to ~25% in a
   decade with no sign of stalling.
3. **China dominates in absolute volume**; the **Rest-of-World** bucket
   (India, SE Asia, Latin America, Africa) shows the highest *relative*
   growth off a small base — the next expansion frontier.
4. Europe and the US show more policy-sensitive, choppier growth, which a
   naive trend forecast wouldn't flag as a risk.

## Possible extensions
- Segment by vehicle type (BEV vs. PHEV) and manufacturer
- Add forecast confidence intervals (bootstrap or Prophet) instead of two
  point-estimate scenarios
- Bring in macro drivers (battery cost curves, policy/subsidy timelines,
  charging infrastructure density) for a causal model instead of pure
  time-series extrapolation
  
## Goal: Understand how the global electric vehicle (EV) market has grown over the last decade, quantify that growth, break it down by region, and build a short-term forecast for 2026–2030.

Pipeline (what each section does and why):

Data Preparation — load & sanity-check the data
Exploratory Data Analysis (EDA) — look before we model
Growth Analysis — YoY growth and CAGR (the "how fast" question)
Forecasting — project 2026–2030 using a couple of models, and compare them
Regional Analysis — who is actually driving the growth
Insights & Recommendations — translate numbers into decisions
