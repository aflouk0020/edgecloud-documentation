# SCRUM-719 Device Heartbeat Management

## Ownership and policy

Device Service owns heartbeat ingestion, policy evaluation, transition persistence, history, statistics, and inventory projection. Monitoring Service telemetry freshness remains independent. API Gateway continues to forward the complete `/api/v1/devices/**` path and apply its existing JWT filter.

The central policy uses the device configuration's heartbeat interval and timeout. With heartbeat age `a`, interval `i`, and timeout `t` (`t > 2i`):

- `UNKNOWN`: no heartbeat has been received.
- `ONLINE`: `a <= i`; the latest heartbeat is within its expected interval.
- `HEALTHY`: `i < a <= 2i`; the connection remains healthy during one tolerated late interval.
- `DELAYED`: `2i < a <= t`; one or more expected heartbeats are missing, but the grace timeout has not elapsed.
- `OFFLINE`: `a > t`.

```text
UNKNOWN --heartbeat--> ONLINE --late--> HEALTHY --later--> DELAYED --timeout--> OFFLINE
                              ^                                             |
                              +--------------- heartbeat -------------------+
```

Status reads are timestamp-derived and do not write. A scheduled evaluator persists changed state/missed counts and the significant `DELAYED` and `OFFLINE` transitions. A subsequent heartbeat transaction records `RECOVERED`, updates `lastRecoveryAt`, resets the missed count, and returns the device to `ONLINE`.

History is paginated and never joined into inventory rows. Configuration is loaded in a batch for each inventory page. History statistics are requested only from the details dialog. The final controlled local policy test performed 10,000 calculations in 7 ms; this is an engineering observation, not a production SLA.

## Security and boundaries

Global heartbeat details require `ADMIN` or `OPERATOR`. `PROJECT_ADMIN` uses project-scoped endpoints, which verify the device association through Project Service. `VIEWER` is denied. Policy changes reuse the established configuration RBAC. Machine heartbeat ingestion retains the existing Gateway JWT architecture; a distinct per-device credential model is not introduced by this story.

No notifications, incidents, remediation, remote commands, or configuration distribution are added.
