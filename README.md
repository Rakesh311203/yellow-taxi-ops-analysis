# yellow-taxi-ops-analysis

# NYC Taxi Fleet Operations Analysis

## Overview
End-to-end operations analysis of 2.8 million NYC Yellow Taxi trips (January 2023)
using Python. Built to demonstrate AI-assisted analysis workflows including data
cleaning, query generation, output validation, and insight communication.

**Tools:** Python · pandas · matplotlib · Claude (AI assist)

---

## Business Questions
Three questions framed from an operations analyst perspective:

1. **When and where is demand highest?**
   Peak hours by day of week and top pickup zones by trip volume

2. **How efficient are trips operationally?**
   Average speed and trip duration patterns across hours and days —
   quantifying congestion impact

3. **Where is revenue-per-mile lowest?**
   Fare efficiency by pickup zone among the top 20 highest-volume locations

---

## Data Source
NYC TLC Trip Record Data — Yellow Taxi, January 2023
[https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page)

Original rows: 3,066,766
Rows after cleaning: 2,876,094

---

## Data Cleaning
Removed ~190K rows based on:
- Implausible trip durations (too short / too long)
- Zero or negative distance trips
- Financial anomalies (negative fares, zero total amount)
- Passenger count outside valid range

AI was used to generate initial cleaning code. Thresholds were set manually
based on operational logic and validated by cross-checking flagged rows.

---

## Key Findings

**Demand**
- [Add your finding — e.g. "Friday 6–8pm accounts for X% of weekly peak volume"]
- Top 3 pickup zones account for disproportionate share of total trips

**Operational Efficiency**
- Average speed drops significantly between [hours] — congestion window
- [Day] shows highest trip duration variance, indicating unpredictable service times

**Fare Efficiency**
- [X] zones fall below median fare-per-mile among top 20 zones
- Short-haul trips in high-congestion zones show the worst revenue-per-mile ratio

---

## How AI Was Used
| Task | AI role | Human validation |
|------|---------|-----------------|
| Cleaning code | Generated pandas logic | Thresholds set manually |
| Analysis queries | Drafted groupby and aggregation code | Logic verified before running |
| Insight framing | First draft of findings | Rewritten with actual numbers |

---

## Files
| File | Description |
|------|-------------|
| `cleaning.ipynb` | Data loading and cleaning pipeline |
| `analysis.ipynb` | All three business question analyses |
| `charts/` | Output visualisations |

---

## What I'd Do Next
- Bring in zone name lookup table to replace Location IDs with readable names
- Extend to 3 months to validate if January patterns are seasonal
- Build a simple demand forecasting model by zone and hour
