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
| **Avg. Absence per Employee** | **7.19 h** |
| **Workforce Size** | 611 employees |
| **Top Reason** | Medical consultation (129 cases) |
| **Peak Month** | **September – 9.8 h** |
| **Peak Day** | **Monday – 8.4 h** |

Key takeaways:

* Medical & dental consultations explain **39 %** of all absences.  
* Healthy-BMI employees miss **≈ 2 hours fewer** than obese peers.  
* Monday spikes suggest weekend spill-over or scheduling issues.


## Insights Deep Dive

### Employee Demographics
* **BMI impact:** Healthy group → 6.0 h vs. Obese → 9.3 h.  
* **Pets & Children:** Pet owners slightly lower; children neutral.

### Seasonal & Weekly Trends
* **Seasonality:** Spring & Autumn > Summer & Winter.  
* **Weekday:** Hours trend downward as the week progresses.

### Reasons for Absence
* Top 3 reasons = medical, dental, musculoskeletal issues.  
* **“Unknown”** reason code appears 39 times → data-quality flag.

### Compensation & Reward Model
* \$1,000 bonus pool for **Low Absence** employees (< 4 h) → 196 staff qualify.  
* **Non-smoker raise simulation:** \$10 k budget = +\$0.48/hr for 312 employees.

### Dashboard Design Notes
The Power BI report uses a four-panel grid:

1. **Headline KPIs & narrative cards**  
2. **Employee & Category visuals** (pie charts)  
3. **Trend lines** by month / weekday with season slicer  
4. **Reasons & Comparisons** (reason table + scatter)

Dark theme + icons echo the original wireframe for quick executive scanning.


## Recommendations
1. Launch a **targeted wellness program** for high-BMI staff.  
2. Trial **flexible scheduling on Mondays** to cut peak absence.  
3. **Expand tele-health partnerships** to reduce in-person medical leave.  
4. Deploy the **bonus & non-smoker raise schemes** quarterly; monitor ROI.  
5. Tighten **reason-code capture** to eliminate “Unknown” entries.


## Assumptions & Caveats
* Single-year snapshot; multi-year trend may differ.  
* Absence hours capped at 8 h to fix data-entry errors.  
* Privacy limits drill-down beyond high-level reason codes.  
* Simulations assume fixed headcount and ignore overtime.  
* Report optimised for desktop Power BI (mobile out-of-scope).


## Next Steps
* Automate monthly ETL → Power BI refresh.  
* Prototype **predictive model** to flag high-risk absentee weeks.  
* Add cost-of-absence calculations for finance partners.

