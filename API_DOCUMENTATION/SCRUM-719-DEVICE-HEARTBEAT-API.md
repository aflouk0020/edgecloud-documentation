# SCRUM-719 Device Heartbeat API

All browser-facing calls use API Gateway and a bearer JWT.

| Method | Path | Purpose |
|---|---|---|
| `POST` | `/api/v1/devices/heartbeat` | Record a heartbeat for an active registered device |
| `GET` | `/api/v1/devices/management/{deviceId}/heartbeat` | Current calculated state |
| `GET` | `/api/v1/devices/management/{deviceId}/heartbeat/history?page=0&size=20` | Newest-first paginated history (`size` 1–100) |
| `GET` | `/api/v1/devices/management/{deviceId}/heartbeat/statistics` | Recorded, recent, recovery, and offline counts |
| `GET` | `/api/v1/devices/management/projects/{projectId}/devices/{deviceId}/heartbeat` | Project-scoped current state |
| `GET` | `/api/v1/devices/management/projects/{projectId}/devices/{deviceId}/heartbeat/history` | Project-scoped history |
| `GET` | `/api/v1/devices/management/projects/{projectId}/devices/{deviceId}/heartbeat/statistics` | Project-scoped statistics |
| `GET` | `/api/v1/devices/inventory?heartbeatStatus=OFFLINE` | Filter inventory by persisted evaluated heartbeat state |

The existing configuration endpoints now accept and return `heartbeatTimeoutSeconds`. It must be greater than twice `heartbeatIntervalSeconds`. Existing search, project, group, tag, pagination, and sort parameters compose with `heartbeatStatus`.

Representative responses use `200`; invalid input uses `400`, missing/inactive lifecycle cases use the existing `404`/`409` handling, unauthenticated access uses `401`, and disallowed/project-crossing access uses `403`.
