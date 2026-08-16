# SCRUM-719 Heartbeat Schema

Flyway `V5__add_device_heartbeat_management.sql` is additive.

- `edge_devices`: `last_recovery_at`, `online_since`, `heartbeat_state`, `consecutive_missed_heartbeats`.
- configuration, version, and template tables: `heartbeat_timeout_seconds` with a backward-compatible 90-second default.
- `device_heartbeat_history`: immutable received/recovered/delayed/offline events, transition states, missed count, event time, and recorded time.
- index `idx_heartbeat_history_device_time` supports newest-first per-device history.
- index `idx_edge_devices_heartbeat_filter` supports active-device and last-heartbeat scans; the state column remains directly filterable by the bounded, paginated inventory query.

History deliberately has no cascading device foreign key so lifecycle deletion cannot erase operational evidence. Operational state changes never delete history.
