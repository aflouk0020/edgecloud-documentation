# SCRUM-720 Device Maintenance Schema

Flyway migration `V6__add_device_maintenance_mode.sql` is additive. Previously applied V1–V5 migrations are unchanged.

## `edge_devices` additions

| Column | Purpose |
|---|---|
| `maintenance_mode` | Current boolean state; default `FALSE` |
| `maintenance_reason` | Optional reason, maximum 500 characters |
| `maintenance_enabled_at` | Latest enable timestamp |
| `maintenance_enabled_by` | Enabling actor UUID |
| `maintenance_scheduled_end_at` | Optional automatic expiry time |
| `maintenance_disabled_at` | Latest manual/automatic end timestamp |
| `maintenance_disabled_by` | Disabling actor UUID; null for automatic expiry |

`idx_device_maintenance_expiry(maintenance_mode, maintenance_scheduled_end_at)` supports the bounded scheduler lookup.

## `device_maintenance_history`

The table stores an identity key, device UUID, `ENABLED`/`DISABLED`/`EXPIRED` action, occurrence time, nullable actor UUID, reason, and scheduled end. `idx_device_maintenance_history_device_time` supports newest-first device history.

History intentionally has no cascading device foreign key. This follows the existing lifecycle evidence pattern and preserves audit history after a device record is removed. Operational changes never delete maintenance, heartbeat, telemetry, lifecycle, or configuration history.

Runtime validation confirmed one successful V6 schema-history row before and after restart and preserved the existing device record.
