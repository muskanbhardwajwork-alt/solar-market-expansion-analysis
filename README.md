
# Solar Market Expansion Analysis

**Business question:** Which Australian states should a residential solar installer prioritise for expansion?

## Data
Clean Energy Regulator (CER) — *Small-scale installation postcode data*, SGU-Solar installations and capacity files (Apr 2001 – Aug 2026, postcode × month).
Source: https://cer.gov.au/markets/reports-and-data/small-scale-installation-postcode-data

## Approach
1. **Data pipeline (Python/pandas):** combined two raw CER files (857,121 postcode-month records), reshaped wide → long, mapped postcodes to states
2. **Data quality:** handled lost leading zeros (NT postcodes), ACT postcodes inside NSW's range, and text-formatted numeric columns
3. **Validation:** rebuilt CER Table 5 from raw data - national totals match in 26/26 years; state-level variance < 0.6%
4. **SQL analysis (SQLite):** CTEs, LAG (YoY growth), SUM OVER (cumulative installs), RANK and NTILE (market ranking)
5. **Forecasting:** 2021–2025 linear trend vs 2026 year-to-date run-rate
6. **New metric:** average system size (kW) = capacity ÷ installations

## Key findings
- NSW, QLD, VIC and WA made up 87% of 2025 installations. All declined in 2025, but the 2026 run-rate is above 2025 levels in every one (+2% to +33%), so the dip does not look structural
- NT, TAS and ACT were the most resilient in 2025 but represent under 4% of national volume
- Average system size roughly doubled in every state between 2015 and 2025

**Recommendation:** prioritise QLD and NSW, then WA and VIC; treat NT/TAS/ACT as small-footprint test markets.

## Limitations
Postcode-based state mapping; 5-point linear trend; annualisation ignores seasonality; recent CER data may be revised; causes of the 2025 dip not analysed.

## Tools
Python (pandas, NumPy, Matplotlib) · SQL (SQLite) · Google Colab
