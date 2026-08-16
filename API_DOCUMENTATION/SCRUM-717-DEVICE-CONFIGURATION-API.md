# SCRUM-717 Device Configuration API

All browser paths use the existing authenticated Gateway `/api/v1/devices/**` route.

| Method | Path | Roles | Result |
|---|---|---|---|
| GET | `/api/v1/devices/management/{deviceId}/configuration` | ADMIN, OPERATOR | Current or non-persisted defaults |
| PUT | `/api/v1/devices/management/{deviceId}/configuration` | ADMIN, OPERATOR | Validated atomic update |
| GET | `/api/v1/devices/management/{deviceId}/configuration/history` | ADMIN, OPERATOR | Newest-first immutable versions |
| POST | `/api/v1/devices/management/{deviceId}/configuration/restore/{version}` | ADMIN, OPERATOR | Restore as a new version |
| POST | `/api/v1/devices/management/{deviceId}/configuration/template/{templateId}` | ADMIN, OPERATOR | Apply template as a new version |
| GET | `/api/v1/devices/management/configuration-templates` | ADMIN, OPERATOR | Platform templates |
| POST | `/api/v1/devices/management/configuration-templates` | ADMIN | Create template |
| PUT | `/api/v1/devices/management/configuration-templates/{templateId}` | ADMIN | Update template |

Intervals accept 5–86,400 seconds (heartbeat maximum 3,600). Environment is `DEVELOPMENT`, `TESTING`, or `PRODUCTION`; log level is `ERROR`, `WARN`, `INFO`, `DEBUG`, or `TRACE`; endpoint is blank or HTTP(S), at most 500 characters; tags are limited to 20 unique values of 50 characters each.

Defaults are polling 60, heartbeat 30, metrics 60, DEVELOPMENT, INFO, no endpoint, and no tags. A default response has version 0 and is not persisted until changed. Every response states `distributionStatus: STORED_ONLY`.
