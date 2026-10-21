# Reliability & Maintenance Performance Analytics

An Excel-based reliability and maintenance analytics project exploring work-order activity, maintenance expenditure, downtime, failure patterns, and asset reliability across a 2025 reporting period.

## Project Overview

This project presents an executive-style maintenance performance dashboard designed to help maintenance and engineering teams monitor asset performance, compare maintenance strategies, and identify areas that may warrant further investigation.

The analysis uses a dataset of **300 work orders** and an asset master covering **12 assets**. Excel is used to organize the maintenance records, summarize performance metrics, and present the findings in an interactive dashboard.

> **Scope note:** The dashboard describes patterns in this project dataset. Findings should be interpreted in context and should not be treated as verified operational conclusions without validating the underlying source data and KPI definitions.

## Dashboard Preview

![Reliability and Maintenance Performance Dashboard](dashboard-screenshot.png)

## Dashboard KPIs

| KPI | Reported result |
|---|---:|
| Total work orders | 300 |
| Maintenance cost | $218,948.23 |
| Total downtime | 793.5 hours |
| Mean Time to Repair (MTTR) | 5.82 hours |
| Mean Time Between Failures (MTBF) | 677.44 hours |
| Availability | 99.2% |

Values are shown as reported by the workbook dashboard; totals and rates depend on the workbook's calculation definitions and reporting assumptions.

## Questions Explored

- Which assets account for the highest maintenance costs?
- Which assets contribute most to recorded downtime?
- How are work orders distributed across breakdown, corrective, and preventive maintenance?
- Which failure modes occur most frequently?
- How do asset-level MTBF, MTTR, availability, and failure counts compare?
- Which assets or failure patterns may deserve closer maintenance review?

## Selected Observations

- **AST-003** is highlighted in the dashboard as having the highest maintenance cost, downtime, and number of failures.
- **AST-004** is highlighted for high downtime and the highest MTTR.
- Preventive maintenance accounts for the largest share of work orders in the dashboard (152 of 300), followed by corrective maintenance (95) and breakdown maintenance (53).
- Bearing failure is the most frequent failure mode shown (25), followed by control failure, electrical fault, and leakage (24 each).

These are descriptive observations from the displayed analysis, not proof of root cause or a prescriptive maintenance plan.

## Tools & Skills

- **Microsoft Excel** — data organization, analysis, and dashboard presentation
- **PivotTables / PivotCharts** — summary analysis across assets, maintenance types, and failure modes
- **Maintenance analytics** — downtime, repair duration, MTBF, MTTR, availability, and cost metrics
- **Data visualization** — KPI cards, comparative charts, and interactive slicers

## Workbook Structure

The workbook contains these worksheets:

- Project_Brief — project scenario, reporting period, and KPI overview
- Maintenance Data — work-order-level maintenance records
- Fact_Table — supporting fact table (hidden in the workbook)
- Asset_Master — asset attributes and operating assumptions
- Pivot Analysis — summarized analysis feeding the dashboard
- Dashboard — executive-style performance dashboard

## Methodology

1. Review the work-order and asset reference tables.
2. Summarize maintenance activity by type and failure mode.
3. Compare asset-level maintenance costs, downtime, failure counts, MTTR, MTBF, and availability.
4. Present the results through KPI cards, charts, and slicers for month, asset, priority, and maintenance type.
5. Use the dashboard to identify patterns that merit further validation or investigation.

## Limitations & Interpretation

- The reporting period is 2025; conclusions are limited to the records and assumptions included in the workbook.
- KPI interpretation depends on the formulas, failure-count logic, and operating-hour assumptions used in the workbook.
- Availability and reliability measures can vary by asset and calculation method. Confirm the workbook formulas and source assumptions before using the values for operational decisions.
- Frequency alone does not establish severity, root cause, or risk. Maintenance priorities should also consider asset criticality, safety, production impact, and engineering assessment.
- Cost values are presented in USD as represented in the workbook.

## Project Files

The Excel workbook and dashboard screenshot are intended to accompany this README in the repository.

---

**Project:** Reliability & Maintenance Performance Analysis  
**Reporting period:** 2025  
**Primary tool:** Microsoft Excel
