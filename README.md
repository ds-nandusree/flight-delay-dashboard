# ✈️ Flight Delay Analytics Dashboard

**A Power BI dashboard analyzing operational flight delay patterns across U.S. carriers and airports — built end-to-end from raw data to a published, themed report.**

![Dashboard Preview](<img width="791" height="446" alt="Screenshot 2026-10-07 093229" src="https://github.com/user-attachments/assets/d05e9d6c-9b1d-4c91-a728-239a080492e0" />
)

---

## 📌 Overview

Flight delays are a textbook operational analytics problem: they cost airlines money, cost passengers trust, and are driven by multiple interacting causes that aren't obvious from raw records alone. This project takes ~1.9 million individual delayed-flight records and distills them into a dashboard that answers three business questions:

1. **Why** are flights delayed — which cause dominates?
2. **Who** is most affected — which airlines underperform?
3. **When** are delays worst — is there a predictable seasonal pattern?

## 🎯 Problem Statement

A raw spreadsheet of millions of flight records is unusable for decision-making — no manager can read it row by row and act on it. This dashboard compresses that volume into a small set of KPIs and visuals that surface the pattern in seconds, the way an operations analyst would present findings to a non-technical stakeholder.

## 📊 Dataset

- **Source:** [Airlines Delay dataset](https://www.kaggle.com/datasets/giovamata/airlinedelaycauses) (Kaggle), originally published by the U.S. Department of Transportation.
- **Scope:** U.S. domestic flights, **2008**, filtered to delayed flights only (~1.9M records).
- **Fields used:** flight date, carrier, origin/destination, scheduled vs. actual times, arrival delay, and five delay-cause columns (carrier, weather, NAS/air-traffic system, security, late aircraft).
- **Note on recency:** this dataset was selected deliberately for its clean structure and detailed cause-level breakdown — ideal for demonstrating the full analytics workflow (cleaning → modeling → DAX → visualization). Findings reflect 2008 operational patterns, not current airline performance.

## 🧹 Data Preparation

- Replaced nulls in the five delay-cause columns with 0 (nulls occur when a flight wasn't delayed; 0 is the semantically correct value for aggregation).
- Constructed a proper `FlightDate` column from separate Year/Month/Day fields using Power Query, enabling time-series analysis.
- Verified data integrity by hand-tracing sample rows to confirm the five delay-cause columns sum to total arrival delay.

## 🧮 Key Measures (DAX)

| Measure | Logic | Purpose |
|---|---|---|
| `Recovered %` | `DIVIDE(COUNTROWS of flights where ArrDelay <= 15, Total delayed flights)` | % of delayed flights that still arrive within 15 min (FAA's on-time threshold) |
| `Avg Arrival Delay` | Average of `ArrDelay` | Headline severity metric |

## 📈 Dashboard Components

| Visual | Type | What it shows |
|---|---|---|
| Delayed Flights | KPI Card | Total delayed flight records in scope |
| Recovered % | KPI Card | Share of delayed flights still arriving within 15 min |
| Avg Arrival Delay | KPI Card | Average delay length in minutes |
| Total Delay Minutes by Cause | Column Chart | Breaks down delay volume by root cause |
| Avg Arrival Delay by Airline | Bar Chart | Compares carriers by average delay severity |
| Avg Arrival Delay by Month | Line Chart | Seasonal severity trend |
| Delayed Flights Count by Month | Line Chart | Seasonal frequency trend (paired with the above) |
| Airline Slicer | Slicer | Cross-filters all visuals by carrier |

## 🔍 Key Insights

- **Late Aircraft Delay is the dominant cause of total delay minutes**, ahead of weather, carrier, security, and air-traffic system (NAS) delays — indicating a cascading effect where one late flight pushes back the next flight using the same aircraft.
- **December is the worst month on both frequency and severity** — more delays happen, and each one is longer on average, ruling out the possibility that severity alone was skewing the "worst month" finding.
- **Regional carriers (e.g., Mesa Airlines/YV) show the highest average arrival delay**, consistent with tighter turnaround schedules on shorter regional routes.
- Only **~37% of delayed flights "recover"** to arrive within 15 minutes of schedule — once a flight is delayed, it mostly stays delayed.

## 🛠️ Tools & Skills Demonstrated

- **Power BI Desktop** — Power Query (ETL), data modeling, DAX, report design
- **Data cleaning:** null handling, type correction, derived date columns
- **DAX:** custom measures using `DIVIDE`, `CALCULATE`, `COUNTROWS`
- **Dashboard design:** KPI-first layout, custom color theme, cross-filtering slicers
- **Analytical reasoning:** validating data assumptions before building (confirmed cause-column logic by hand-tracing rows), correcting scope-based mislabeling (dataset contains delayed flights only, not all flights)

## ⚠️ Limitations & Honest Scope Notes

- Single flat table — no relational model (e.g., no separate Airports table for geographic analysis).
- Single-page report — no drill-through or bookmark-based navigation.
- Dataset reflects 2008 conditions; not a live or current operational view.
- Delay-cause data is only recorded for flights that were already delayed — the dashboard cannot speak to on-time flights.

*(Documenting limitations deliberately — knowing what a dataset can't tell you is part of doing the analysis correctly.)*

## 📁 Repository Contents

- `dashboard-preview.png` — dashboard screenshot
- `FlightDelayDashboard.pdf` — exported static report

## 🙋 About Me

Built by **Nandusree Diguvasadum**, B.Tech CSE student focused on Data Science & ML, as a self-directed Power BI learning project.
[LinkedIn](https://www.linkedin.com/in/diguvasadum-nandusree/) · [Portfolio](https://ds-nandusree.github.io/portfolio/) · [GitHub](https://github.com/ds-nandusree)
