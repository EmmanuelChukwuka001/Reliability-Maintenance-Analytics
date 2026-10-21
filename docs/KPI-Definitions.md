# KPI Definitions & Interpretation

This document describes common reliability and maintenance KPIs used in the project. The Excel workbook is the source of the reported dashboard values. Where the workbook uses a specific calculation, retain that definition and verify it against the formulas before comparing the result with other reports.

## Work-order volume

**Definition:** Count of work-order records in the selected reporting scope.

**Interpretation:** Indicates recorded maintenance workload. A work order is not necessarily equivalent to a unique failure event; one event may generate multiple work orders, depending on the source process.

## Maintenance cost

**Definition:** Sum of the maintenance cost values included in the selected scope.

**Interpretation:** Compare costs alongside asset criticality, work type, downtime, and production or safety impact. Confirm currency, cost components, and whether values represent actuals, estimates, or budgeted amounts.

## Downtime

**Definition:** Sum of recorded downtime duration for the selected records, expressed in hours.

**Interpretation:** Downtime totals depend on how duration is captured and whether overlapping events are counted separately. Validate the source field and aggregation rules before operational use.

## Mean Time to Repair (MTTR)

A common definition is:

**MTTR = Total corrective repair time ÷ Number of repair events**

Confirm whether the workbook includes only corrective repairs or a broader set of work orders, and whether incomplete or zero-duration records are excluded.

## Mean Time Between Failures (MTBF)

A common definition is:

**MTBF = Total operating time ÷ Number of failures**

MTBF generally applies to repairable assets and depends on a defensible operating-time denominator and failure-event count. Do not assume that work-order count equals failure count.

## Availability

A commonly used inherent-availability approximation is:

**Availability = MTBF ÷ (MTBF + MTTR) × 100%**

Other availability measures may use scheduled time, operating time, planned downtime, or unplanned downtime. Use the exact workbook definition when interpreting the dashboard; do not substitute this formula unless it matches the workbook's method.

## Failure-mode frequency

**Definition:** Count of records associated with each recorded failure mode.

**Interpretation:** Frequency alone does not establish risk or root cause. Prioritization should also consider severity, asset criticality, safety, production impact, and engineering assessment.

## Filters and reporting scope

Dashboard values may change with month, asset, priority, and maintenance-type selections. When comparing values, use the same filter scope and reporting period.

## Validation checklist

Before using these KPIs for operational decisions:

- Trace each KPI to its Excel formula or PivotTable source.
- Confirm the reporting period and filter context.
- Verify units, currency, missing values, and duplicate records.
- Confirm how failures, repairs, operating hours, and downtime are counted.
- Reconcile totals to the underlying work-order records.
- Treat dashboard observations as descriptive until reviewed by a qualified maintenance or reliability professional.
