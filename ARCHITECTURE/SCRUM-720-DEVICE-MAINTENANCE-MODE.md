# SCRUM-720 Device Maintenance Mode Architecture

## Business and operational purpose

Maintenance mode tells operators that a registered device is intentionally unavailable for planned work. Device Service owns this operational context, its scheduling, audit identity, and history.

Maintenance does not change the independent dimensions of device state:

- **Lifecycle:** active/inactive/deleted registration state.
- **Heartbeat:** `ONLINE`, `HEALTHY`, `DELAYED`, `OFFLINE`, or `UNKNOWN` connectivity derived by SCRUM-719.
- **Maintenance:** intentional operator context, active or inactive.

A device may therefore be active, in maintenance, and still send healthy heartbeats. Maintenance never deletes telemetry, heartbeat history, configuration, groups, tags, registration data, or lifecycle history.

## Boundary from Sprint 8

SCRUM-720 is not the Sprint 8 Alert Service maintenance-window feature. Alert maintenance windows suppress alert evaluation for scoped time ranges. Device maintenance mode describes the operational intent of one registered device. No Alert Service suppression semantics, records, or APIs are duplicated in Device Service.

## State model

```text
NOT_IN_MAINTENANCE
       |
       | ADMIN/OPERATOR enable(reason, optional end)
       v
    MAINTENANCE
       |       |
       |       +-- scheduled end reached --> NOT_IN_MAINTENANCE + EXPIRED
       |
       +---------- manual disable --------> NOT_IN_MAINTENANCE + DISABLED
```

Enable records `ENABLED`. Manual disable records `DISABLED`. The scheduler ends due maintenance and records `EXPIRED` once. Exact duplicate enable and repeated disable are no-ops; an incompatible re-enable is a `409` conflict.

## Transaction and audit design

Enable/disable use the existing pessimistic device lookup and a single transaction to change state and append history. History is durable and append-only through application APIs. Actor identity is the authenticated user UUID. Automatic expiry uses a null actor to identify the system action and runs on the existing scheduling foundation at a configurable fixed delay.

Project-scoped controllers reuse `ProjectScopeClient.requireDeviceAssociation`; JWT parsing and role enforcement reuse existing Device Service security. No duplicate authentication or project-ownership subsystem was introduced.

## Boundaries and limitations

- no scheduled future start
- no remote configuration distribution
- no remote commands or automated remediation
- no firmware operations
- no Alert Service maintenance-window duplication
- actor display currently uses UUID rather than a resolved user name
- interactive browser screenshot validation remains **PENDING MANUAL CAPTURE**
