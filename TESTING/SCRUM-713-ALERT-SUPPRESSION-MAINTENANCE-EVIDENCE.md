# SCRUM-713 Alert Suppression and Maintenance Evidence

## Acceptance design

| Requirement | Evidence |
|---|---|
| Window CRUD and expiry | Project-scoped V2 API; enabled flag plus authoritative inclusive-start/exclusive-end evaluation. |
| Project/service/device scopes | Source matching and Project workspace association validation. |
| Monitoring continuity | Suppression occurs only inside Alert lifecycle generation, after Monitoring persistence and rule evaluation. |
| No downstream delivery | Matching triggered condition records suppression and returns before AlertEvent/outbox construction. |
| History and audit | Dedicated immutable suppression snapshots and create/update/disable actor audit. |
| Isolation and RBAC | Project-qualified queries; authenticated read; ADMIN/PROJECT_ADMIN-only mutation; VIEWER/OPERATOR denied. |
| Duplicate protection | Deterministic SHA-256 identity plus database unique constraint. |

Flyway V7 creates `maintenance_windows`, `alert_suppression_history`, `maintenance_window_audit`, time/scope lookup indexes, range/scope checks, history foreign key, and suppression uniqueness.

## Automated validation

- Alert Service: 124/124 tests passed, including MySQL 8.4 migration/concurrency tests.
- API Gateway: 6/6 tests passed and package built.
- Dashboard: 160/160 tests passed and the production bundle built.
- Monitoring Service: 68/68 regression tests passed.
- Notification Service: 56/56 regression tests passed.
- Device Service: 18/19 passed; one pre-existing controller test uses an expired fixed JWT and returned 401 instead of its expected 200. Runtime device registration/association was successful and no Device source changed.

## Controlled Docker acceptance evidence

All 15 Compose containers were healthy and the seven discoverable applications were `UP` in Eureka. Alert Flyway V7 had exactly one successful history row.

- An active project window produced one evaluated/triggered condition, zero AlertEvents, zero outbox entries, zero emails, and suppression evidence. Two deliberately overlapping project windows produced two history rows; replaying the identical sample produced zero additional rows.
- Monitoring accepted telemetry with HTTP 201 and `telemetry_metrics` increased by one during the active window.
- SERVICE and DEVICE matching each produced one suppression and zero AlertEvents. Their non-matching sources each produced one normal AlertEvent.
- A four-second window suppressed before its end, derived `EXPIRED` afterward, then allowed a new AlertEvent. Its OPENED outbox was `PUBLISHED`, produced two recipient notifications and four `DELIVERED` in-app/email channel records.
- A separately created Project B had zero windows/suppressions and independently produced one AlertEvent and one outbox entry.
- Gateway returned 401 without a token and 403 for VIEWER mutation; project target association validation used Project Service workspace ownership.

This is controlled local Docker/MySQL/Mailpit acceptance evidence, not a production throughput claim or SLA. Manual screenshots remain **PENDING MANUAL CAPTURE**.
