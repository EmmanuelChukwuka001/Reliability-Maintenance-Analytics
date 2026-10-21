# KPI Definitions & Interpretation

This document reflects the DAX measures shown in the project's Power BI **Manage Measures** view. It distinguishes the measures implemented in the model from general industry definitions. Values can change with report filters and the current evaluation context.

## Core measures implemented in the model

### Total Work Orders
**DAX:** `COUNTROWS(Maintenance_Data)`

Counts rows in `Maintenance_Data` in the current filter context. This is a row count, so it represents distinct work orders only if each row corresponds to one unique work order.

### Total Maintenance Cost
**DAX:** `SUM(Maintenance_Data[Total_Maintenance_Cost_USD])`

Sums the maintenance cost field. The model labels the field in USD; confirm the source data's currency and what cost components are included before comparing with other reports.

### Total Downtime
**DAX:** `SUM(Maintenance_Data[Downtime_Hours])`

Sums recorded downtime hours in the current filter context.

### Average Downtime
**DAX:** `AVERAGE(Maintenance_Data[Downtime_Hours])`

Calculates the arithmetic mean of the row-level downtime values. This is not the same as total downtime and may include zero or blank values according to DAX's standard aggregation behavior (blank values are ignored).

### Total Failures
**DAX:** `SUM(Maintenance_Data[Failure_Count])`

Sums the failure-count field. This measure depends on the source data's definition of a failure event; it is not necessarily equal to the number of work-order rows.

### Total Labour Hours
**DAX:** `SUM(Maintenance_Data[Labour_Hours])`

Sums recorded labour hours.

### Total Operating Hours
**DAX:** `(8760 * DISTINCTCOUNT(Maintenance_Data[Asset_ID])) - [Total Downtime]`

Estimates total operating hours by subtracting recorded downtime from 8,760 hours per distinct asset. This assumes a full 8,760-hour year for each asset in scope. The formula does not adjust for a partial reporting period, commissioning dates, planned operating schedules, or overlapping downtime records; confirm those assumptions before interpreting it as actual operating time.

### MTBF
**DAX:** `DIVIDE([Total Operating Hours], [Total Failures])`

Calculates estimated operating hours per recorded failure. The result depends on the operating-hours assumption above and on the definition and completeness of `Failure_Count`. If the denominator is zero or blank, `DIVIDE` returns blank unless an alternate result is supplied.

### MTTR
**DAX:** `DIVIDE(SUM(Maintenance_Data[Repair_Hours]), SUM(Maintenance_Data[Failure_Count]))`

Calculates recorded repair hours per recorded failure count. This is a failure-count-weighted ratio, not necessarily the average repair duration per work order. Its interpretation depends on how repair hours and failure counts are populated.

### Availability
**DAX:** `DIVIDE([Total Operating Hours], 8760 * DISTINCTCOUNT(Maintenance_Data[Asset_ID]))`

Calculates estimated operating hours divided by 8,760 hours per distinct asset. The result is a ratio (multiply by 100 to express it as a percentage if the visual does not already format it as a percentage). It is based on the model's annual-hours assumption and the downtime subtraction used in `[Total Operating Hours]`; it is not the MTBF/(MTBF + MTTR) formula.

## Maintenance-type measures

These measures calculate each maintenance type's share of work-order rows:

- **Preventive Maintenance %:** count of rows where `Maintenance_Type = "Preventive"` divided by `[Total Work Orders]`.
- **Corrective Maintenance %:** count of rows where `Maintenance_Type = "Corrective"` divided by `[Total Work Orders]`.
- **Breakdown Maintenance %:** count of rows where `Maintenance_Type = "Breakdown"` divided by `[Total Work Orders]`.

These percentages describe the mix of recorded work orders, not the share of cost, labour, downtime, or failures. They may not total 100% if some rows have blank or other maintenance-type values.

## Concern flags and priority score

The model creates four percentile-based concern flags:

- **Availability Concern:** 1 when `[Availability]` is at or below the 25th percentile of `[Availability]` across `ALL(Maintenance_Data[Asset_ID])`; otherwise 0.
- **MTBF Concern:** 1 when `[MTBF]` is at or below its 25th percentile across all asset IDs; otherwise 0.
- **MTTR Concern:** 1 when `[MTTR]` is at or above its 75th percentile across all asset IDs; otherwise 0.
- **Cost Concern:** 1 when `[Total Maintenance Cost]` is strictly above its 75th percentile across all asset IDs; otherwise 0.
- **Failure Concern:** 1 when `[Total Failures]` is at or above its 75th percentile across all asset IDs; otherwise 0.

These are relative screening flags, not absolute engineering limits. The DAX uses `PERCENTILEX.INC` and `ALL(Maintenance_Data[Asset_ID])`; confirm how each measure evaluates at asset and total level, and whether the percentile population matches the intended asset-level comparison.

**Priority Score** sums the five concern flags: MTBF Concern, MTTR Concern, Availability Concern, Failure Concern, and Cost Concern. A higher score means more of these relative flags are triggered; it does not directly measure risk or prove root cause.

**Priority State** is assigned using `SWITCH(TRUE())`:
- **HIGH:** Priority Score ≥ 4
- **MEDIUM:** Priority Score ≥ 2 and < 4
- **NORMAL:** Priority Score < 2

Use this state as a prioritization aid only. Maintenance decisions should also consider asset criticality, safety, production impact, failure severity, and engineering review.

## Filter context and interpretation

The measures respond to the report's filter context. When comparing assets or periods, keep filters consistent and confirm whether calculations are evaluated at individual asset, category, or total level. In particular, the operating-hours measures assume a full year for each distinct asset in the current context.

## Validation checklist

Before using the dashboard for operational decisions:

- Confirm that each row represents the expected work-order grain and check for duplicate work-order IDs.
- Verify currency and the definition of maintenance cost.
- Confirm whether downtime and repair hours are measured in hours and whether overlapping events are possible.
- Validate the 8,760-hours-per-asset assumption against the actual reporting period and operating schedule.
- Verify the meaning and counting logic of `Failure_Count`; it is the denominator for both MTBF and MTTR.
- Check whether the availability visual formats the ratio as a percentage.
- Inspect the percentile flags at asset and total level and confirm that the percentile population is appropriate.
- Treat concern flags and priority states as descriptive screening rules, not as validated risk classifications or root-cause analysis.
