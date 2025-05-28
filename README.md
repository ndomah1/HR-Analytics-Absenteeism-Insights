# HR Analytics — Absenteeism Insights

> **Purpose:** Equip HR leaders with data-driven insight into why, when and how employees are absent—so they can design smarter wellness, scheduling and compensation policies.


## Table of Contents
- [Dashboard Preview](#dashboard-preview)
- [Project Background](#project-background)
- [Data Structure & Initial Checks](#data-structure--initial-checks)
- [Executive Summary](#executive-summary)
- [Insights Deep Dive](#insights-deep-dive)
  - [Employee Demographics](#employee-demographics)
  - [Seasonal & Weekly Trends](#seasonal--weekly-trends)
  - [Reasons for Absence](#reasons-for-absence)
  - [Compensation & Reward Model](#compensation--reward-model)
  - [Dashboard Design Notes](#dashboard-design-notes)
- [Recommendations](#recommendations)
- [Assumptions & Caveats](#assumptions--caveats)
- [Next Steps](#next-steps)

## Dashboard Preview

![dashboard](https://github.com/ndomah1/HR-Analytics-Absenteeism-Insights/blob/main/images/HR%20Analytics%20Dashboard.png)


## Project Background
As part of an HR modernization initiative, I was asked to build an end-to-end analytics solution that answers two strategic questions:

1. **How can we proactively reward healthy employee behaviour?**  
2. **Where are the biggest drivers of absenteeism, and how can we mitigate them?**

Using SQL Server for data prep and Power BI for visualisation, I produced an executive-ready, dark-themed dashboard that slices absenteeism by season, weekday, reason code and demographic attributes.


## Data Structure & Initial Checks
| File | Description |
|------|-------------|
| [`Absenteeism_at_work.csv`](https://github.com/ndomah1/HR-Analytics-Absenteeism-Insights/blob/main/data/Absenteeism_at_work.csv) | Raw absence records (dates, hours, reason codes) |
| [`Reasons.csv`](https://github.com/ndomah1/HR-Analytics-Absenteeism-Insights/blob/main/data/Reasons.csv) | Lookup table: reason code → description |
| [`Compensation.csv`](https://github.com/ndomah1/HR-Analytics-Absenteeism-Insights/blob/main/data/compensation.csv) | Base pay and smoker status for each employee |

**Pre-processing steps**

* Parse dates into `Month`, `Season`, `Weekday`.
* Categorise **BMI** (Underweight / Healthy / Overweight / Obese).
* Bin **Absence Hours** into **Low** (< 4 h), **Moderate** (4–8 h), **High** (> 8 h).
* Create a non-smoker flag for wage-increase simulation.

Cleaned tables were imported into Power BI via SQL views.


## Executive Summary
| KPI | Value |
|-----|-------|
| **Avg. Absence per Employee** | **6.92 h** |
| **Workforce Size** | 740 employees |
| **Total Hours Lost** | 5 124 h |
| **Top Reason** | Medical consultation (149 cases) |
| **Peak Month** | **July (10.95 h)** |
| **Peak Day** | **Day 2 (likely Monday) – 9.25 h** |

Key takeaways:

* **Medical & dental consultations account for ~35 %** of all recorded absences (149 + 112 of 740 cases).  
* A majority of staff fall in the **Healthy BMI bracket (53 %)**, but Obese (28 %) and Over-weight (20 %) cohorts remain substantial.  
* Absenteeism spikes in **mid-summer (July)** and at the **start of the work-week (Day 2),** indicating potential scheduling and wellness opportunities.


## Insights Deep Dive

### Employee Demographics
* **BMI mix:** Healthy = 390 (53 %); Over-weight = 146 (20 %); Obese = 204 (28 %).  
* **Pets & Children:** No dramatic absenteeism swing, though employees with *no* pets or children trend slightly higher.

### Seasonal & Weekly Trends
* **Seasonality:** Summer (esp. July) shows the sharpest uptick, with winter months comparatively low.  
* **Weekday:** Hours decline steadily from Day 2 to Day 5, then tick up slightly on Day 6.

### Reasons for Absence
| Rank | Reason | Count |
|------|--------|-------|
| 1 | Medical consultation | **149** |
| 2 | Dental consultation | **112** |
| 3 | Physiotherapy | **69** |
| 4 | Musculoskeletal diseases | **55** |
| 5 | Unknown | **43** |

> Combined, the top two categories drive roughly one-third of all absence events.

### Compensation & Reward Model
* \$1 000 bonus pool for **Low-Absence** employees (< 4 h) remains cost-effective given the improved average.  
* **Non-smoker raise simulation** (budget = \$10 K) continues to show a modest hourly uplift while favouring 300+ employees.

### Dashboard Design Notes
The Power BI report uses a four-panel grid:

1. **Headline KPIs & narrative cards**  
2. **Employee & Category visuals** (pie/donut charts)  
3. **Trend lines** by month / weekday with season slicer  
4. **Reasons & Comparisons** (reason table + workload vs transportation scatter)

Dark mode, iconography and concise tooltips ensure quick executive scan-ability.


## Recommendations
1. **Target July** with wellness campaigns and optional WFH to offset the seasonal spike.  
2. **Offer preventive healthcare credits** to cut medical/dental absences (~35 % of total).  
3. **Pilot flexible scheduling on Day 2 (Monday)** where average hours peak at 9.25 h.  
4. Roll out the **bonus & non-smoker wage incentives** and evaluate quarterly ROI.  
5. Improve data capture to reduce **“Unknown”** reason code instances (43 cases).


## Assumptions & Caveats
* Analysis covers **one calendar year**; multi-year variance not assessed.  
* Absence hours capped at one shift (8 h) for outlier correction.  
* Privacy rules limit drill-down beyond high-level reason codes.  
* Simulations assume constant headcount and ignore overtime.  
* Report optimised for desktop Power BI; mobile view out-of-scope.


## Next Steps
* Automate monthly ETL → Power BI refresh.  
* Build a **predictive model** to flag high-risk weeks ahead of time.  
* Integrate **cost-of-absence** metrics to quantify productivity impact for Finance.
