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
Key insights
<img width="2084" height="1482" alt="q1_demand" src="https://github.com/user-attachments/assets/adda5157-6672-402c-afe1-0c5cd0c7e7fd" />
<h2>Trip Demand and Pickup Zones</h2>
What the data shows: Taxi demand heavily clusters during mid-week evening rush hours (Tuesday–Thursday, 5:00 PM–7:00 PM), peaking at over 35,000 trips per hour, while dropping to fewer than 5,000 trips during early morning periods (4:00 AM–5:00 AM). Spatially, a single outer-borough transit hub—Zone 132 (JFK Airport)—dominates absolute volume with over 160,000 individual pickups, significantly outpacing core Manhattan hubs like Zone 237 (Upper East Side South) at roughly 148,000 trips.

Why it matters: The massive mid-week evening spike creates immediate driver supply deficits in Manhattan, whereas the outsized, constant volume at JFK requires persistent, high-capacity taxi holding queues away from the city center to handle deplaning passenger surges without blocking airport loop traffic.

What can be done: Implement a targeted "Mid-Week Rush" driver incentive bonus between 5:00 PM and 7:00 PM on Tuesday through Thursday to increase active fleet capacity, paired with an automated dispatch alert system that redirects empty vehicles to the JFK holding lot whenever flight arrivals exceed 15 major landings within a 60-minute window.

<img width="2084" height="732" alt="q2_efficiency" src="https://github.com/user-attachments/assets/831f96b3-a3d8-46b4-981a-0f9471ce8840" />
<h2>Speed and Duration Efficiency</h2>h2>
What the data shows: Average speeds severely collapse into a "Congestion Window" below 18.5 mph across almost the entire active daytime tracking window. Meanwhile, daily trip durations across the week show remarkable consistency, maintaining a tight median of approximately 11 to 12 minutes per trip across all seven days, with Thursday experiencing slightly wider variability and the highest overall upper-quartile trip lengths (stretching past 19 minutes).

Why it matters: The systemic drop in daytime speed severely restricts vehicle utilization rates, meaning an individual taxi can complete fewer passenger loops per shift. However, because median durations remain stable even on weekends, the total earning potential per hour stays predictable for drivers, despite the localized gridlock.

What can be done: Shift fleet deployment strategies away from short Manhattan zone cruising during the daytime congestion window, and instead incentivize drivers to position for longer-distance highway routes where they can maintain speeds above the 18.5 mph threshold to maximize mileage revenue.

<img width="1784" height="1032" alt="q3_fare_efficiency" src="https://github.com/user-attachments/assets/821b0902-caad-4c52-a1fe-04e652658129" />
<h2>Fare Efficiency by Pickup Zone</h2>
What the data shows: There is a distinct economic split across the top 20 busiest regions, bisected by a median value of $9.20 per mile. Zone 132 (JFK Airport) leads the fleet in financial yield, generating a high average of over $10.50 per mile, while Zone 138 (LaGuardia Airport) sits at the bottom of the top tier, yielding an average of only $7.40 per mile.

Why it matters : Not all high-volume zones are equally profitable. While both JFK and LaGuardia process vast amounts of travelers, JFK's higher fare per mile (likely driven by flat-rate airport pricing structures and lower idling time on highways) represents a vastly more lucrative dispatch destination for drivers than LaGuardia's shorter, traffic-prone routes into the city.

What can be done: Revise the airport dispatch queue priority algorithm to award "Short Trip tokens" to drivers completing lower-yield LaGuardia runs, allowing them to skip to the front of the high-yield JFK pickup queue on their next airport return to balance out driver earnings across the fleet.
