# MyZubster LIFE 2026 — Baseline & MRV Framework

> Public-safe working framework derived from the internal Baseline & MRV v0.1. Status: pre-candidature. Quantitative targets remain **TBD until measured and validated**.

## Purpose

Define a transparent baseline, monitoring, reporting and verification system that can compare initial conditions with post-intervention performance while preserving traceability of sources, assumptions, calculations and evidence.

```text
BASELINE
  → INTERVENTION
  → MONITORING
  → KPI CALCULATION
  → VERIFICATION
  → RESULT
  → REPLICATION
```

## MRV principles

- No environmental value is assumed without an identifiable source.
- Missing values remain `TBD` until measured or validated.
- Every KPI must have a unit, formula, source, frequency, responsible owner and associated evidence.
- Before/after comparisons must be normalized where weather, surface area, duration, seasonality or operational intensity affect comparability.
- Manual data and IoT data must remain distinguishable.
- Corrections, exclusions and anomalies must remain in the audit trail.
- Final methodology should be validated by an appropriate scientific/environmental partner.

## Pilot analysis unit

Before launch, the project must identify and document:

- pilot site and authorization status;
- site/operator responsibility;
- relevant area or operational unit;
- activity/vegetation/process type;
- baseline period;
- demonstration period;
- sensors/technologies used;
- comparison method, ideally including a control where feasible.

## Water baseline

Candidate data fields:

- total water volume;
- volume per intervention;
- serviced area;
- water source;
- date, time and duration;
- relevant weather/precipitation;
- soil moisture where available;
- vegetation/process type;
- known losses/anomalies;
- existing decision process.

Candidate KPIs:

- `A1` — water volume per hectare / period;
- `A2` — water volume per intervention;
- `A3` — normalized percentage water saving vs baseline;
- `A4` — interventions avoided/optimized without deteriorating the operational outcome.

Baseline and target values remain `TBD`.

## Operational baseline

Possible inputs include intervention count, person-hours, machine-hours, relevant travel, intervention duration, extraordinary calls, failures and preventive/corrective maintenance.

Candidate KPIs include interventions per area, operational hours per area, reduction of unnecessary interventions and reduction of anomalous/extraordinary interventions where causal attribution is credible.

## Materials and circularity baseline

Possible inputs:

- replaced components/materials;
- quantity or mass by type;
- reason for replacement;
- repairs and reuse;
- observed/estimated useful life;
- documented waste generation/destination;
- relevant replacement purchases.

Candidate KPIs:

- avoided material/waste quantity;
- repair/reuse rate;
- documented useful-life increase;
- reduction in replacements versus normalized baseline.

## Energy guardrail

The project should account for energy introduced by sensors, gateways, communications, processing or optional automation.

Candidate measures include:

- additional system kWh per period;
- net energy avoided or added, only when a validated calculation method exists.

## Data quality

Each data flow should record:

- source ID;
- data owner/responsible party;
- acquisition method (`sensor`, `API`, `manual`, `documentary`);
- frequency and unit;
- timestamp;
- completeness;
- validation state;
- anomaly/outlier handling;
- sensor version/calibration where relevant;
- authorization and usage restrictions.

Candidate data-quality KPIs:

- `D1` — percentage of complete records;
- `D2` — percentage of validated records;
- `D3` — percentage of period covered by usable data;
- `D4` — number of documented corrections/anomalies.

## Evidence classes

Depending on the KPI, evidence may include:

- meter readings;
- sensor/API exports;
- MyZubster logs;
- operational registers;
- maintenance/technical records;
- appropriate dated or georeferenced photographs;
- identified weather datasets;
- operator reports;
- scientific/technical validation minutes;
- versioned methodology and calculation files.

## Normalization

Before declaring improvement, assess at minimum:

- area;
- number/days of activity;
- precipitation and temperature;
- seasonality;
- vegetation/process type;
- infrastructure changes independent from the intervention;
- failures or exceptional events.

General working formula:

```text
Improvement % =
((Normalized baseline - Normalized pilot value) / Normalized baseline) × 100
```

The exact formula for each KPI should be frozen before final evaluation.

## Quality gate

**GO** only if the site is identified and authorized, baseline is available or measurably obtainable, at least one primary environmental KPI is quantifiable, data ownership is clear, and the measurement protocol is approved.

**HOLD** when data gaps are limited and recoverable within the project schedule.

**NO-GO** for a site when a credible baseline cannot be produced or the result cannot reasonably be attributed to the intervention.

## Expected MRV outputs

- Baseline Report
- Data Dictionary
- Measurement Protocol
- KPI Register
- Data Quality Log
- Pilot Monitoring Dashboard
- Verification Report
- Replication Dataset / Toolkit subject to ownership, privacy and security constraints

MyZubster-specific indicators may complement but do not replace applicable official LIFE indicators.
