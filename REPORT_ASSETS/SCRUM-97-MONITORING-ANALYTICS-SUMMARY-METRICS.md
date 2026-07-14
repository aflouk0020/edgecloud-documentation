# SCRUM-97 — Monitoring Analytics and Summary Metrics

## Purpose

SCRUM-97 extends EdgeCloud Monitor with higher-level operational analytics. The implementation aggregates existing service-monitoring, telemetry, device, and alert records into deterministic summary metrics that are presented through the authenticated React dashboard.

## Architecture

Analytics remain owned by the microservice responsible for the source data:

- Monitoring Service: service uptime, response latency, and telemetry averages.
- Device Service: online/offline fleet counts and availability percentage.
- Alert Service: active/resolved totals and severity distribution.
- React Dashboard: retrieves the three summaries through the API Gateway and presents a consolidated analytics view.

No database schema changes were required. All metrics are derived from existing persisted records.

## API Endpoints

| Gateway endpoint | Purpose |
| --- | --- |
| `GET /api/v1/monitoring/analytics` | Service availability, latency, and telemetry averages |
| `GET /api/v1/devices/summary` | Device availability and online/offline totals |
| `GET /api/v1/alerts/summary` | Alert lifecycle and severity totals |

All requests use the existing JWT authentication workflow.

## Analytics Calculations

- Service uptime percentage: `(UP checks / total service checks) × 100`.
- Average response time: arithmetic mean of recorded response times.
- Device availability percentage: `(online devices / registered devices) × 100`.
- Telemetry averages: arithmetic mean of recorded CPU, memory, and temperature samples.
- Alert summaries: counts grouped by active/resolved status and LOW/MEDIUM/HIGH severity.
- Empty datasets return zero-valued summaries instead of calculation errors.
- Decimal values are rounded to two decimal places for stable API and dashboard presentation.

## Validation Evidence

The following live API responses were verified through the API Gateway on 14 July 2026:

```json
{
  "totalServiceChecks": 5,
  "upServiceChecks": 0,
  "downServiceChecks": 5,
  "serviceUptimePercentage": 0.0,
  "averageResponseTimeMs": 2020.4,
  "telemetrySamples": 19,
  "averageCpuUsage": 39.6,
  "averageMemoryUsage": 46.7,
  "averageTemperature": 49.36
}
```

```json
{
  "totalDevices": 2,
  "onlineDevices": 1,
  "offlineDevices": 1,
  "availabilityPercentage": 50.0
}
```

```json
{
  "totalAlerts": 5,
  "activeAlerts": 3,
  "resolvedAlerts": 2,
  "lowSeverityAlerts": 0,
  "mediumSeverityAlerts": 2,
  "highSeverityAlerts": 3
}
```

## Automated Verification

- Monitoring Service tests passed, including analytics calculation and empty-data scenarios.
- Device Service tests passed, including fleet availability and zero-device scenarios.
- Alert Service tests passed, including lifecycle and severity aggregation.
- React dashboard lint passed.
- React dashboard production build passed.
- React dashboard test suite passed: 17 tests across 5 test files.
- Dashboard tests cover successful aggregation, partial API failure, and refresh behaviour.

## Dashboard Evidence

Manual acceptance testing confirmed:

- platform KPI cards display service uptime, average response time, device availability, and active alerts;
- telemetry cards display average CPU, memory, and temperature;
- resolved-alert totals are visible;
- service-check, device-availability, and alert-severity distributions are displayed;
- the Refresh Analytics action reloads live values;
- the layout remains readable across the complete scrollable dashboard;
- screenshots were collected for the KPI, telemetry-average, and operational-composition sections.

## Acceptance Criteria Traceability

| Acceptance criterion | Evidence | Status |
| --- | --- | --- |
| AC1 — Service uptime metrics | Monitoring analytics endpoint and service-check distribution | Passed |
| AC2 — Average response time | Monitoring analytics endpoint and performance KPI | Passed |
| AC3 — Device availability | Device summary endpoint, KPI, and fleet distribution | Passed |
| AC4 — Alert summaries | Alert summary endpoint, counters, and severity distribution | Passed |
| AC5 — Telemetry summaries | CPU, memory, and temperature averages | Passed |
| AC6 — Dashboard analytics | Manual dashboard acceptance and automated component tests | Passed |

## Outcome

SCRUM-97 provides a consolidated, explainable analytics layer without duplicating source data or coupling microservices. The resulting dashboard improves operational awareness and final-demonstration quality while preserving the existing service boundaries and API Gateway architecture.
