# Sprint 9 Device Registration and Lifecycle API

The Device Service exposes lifecycle operations through the existing Gateway device route. The Gateway strips `/api/v1/devices`, so browser requests below reach Device Service `/management` paths without a new route.

| Method | Gateway path | Roles | Purpose |
|---|---|---|---|
| POST | `/api/v1/devices/management` | ADMIN | Register a unique device |
| GET | `/api/v1/devices/management/{deviceId}` | ADMIN, OPERATOR | Read lifecycle metadata |
| PUT | `/api/v1/devices/management/{deviceId}` | ADMIN, OPERATOR | Replace supported metadata |
| POST | `/api/v1/devices/management/{deviceId}/deactivate` | ADMIN, OPERATOR | Make the device inactive and offline |
| POST | `/api/v1/devices/management/{deviceId}/reactivate` | ADMIN, OPERATOR | Return it to active; heartbeat determines online state |
| DELETE | `/api/v1/devices/management/{deviceId}` | ADMIN | Remove an already inactive local record |
| GET | `/api/v1/devices/management/{deviceId}/history` | ADMIN, OPERATOR | Read newest-first lifecycle history |

Registration and update accept `name`, `type`, `ipAddress`, `description`, `location`, `firmwareVersion`, and `operatingSystem`. Name, type, and IP address are mandatory. Duplicate names and invalid state transitions return `409`; validation returns `400`; missing devices return `404`; unauthenticated and insufficient-role requests return `401` and `403`.

Deletion is deliberately local and guarded: active devices must first be deactivated. Immutable lifecycle history has no cascading foreign key and survives removal. Telemetry, project associations, and alert records are owned by other services and are never deleted by this API.

Project assignment remains owned by Project Service. No cross-service database foreign key or fabricated project value was added.
