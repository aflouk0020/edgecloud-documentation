# SCRUM-718 Device Organisation API

All operations require a bearer JWT and are routed through the Gateway under `/api/v1/devices`. Group and tag resources are scoped by the logical Project Service project ID. Device Service forwards the bearer token to Project Service to verify project access and active device association; it does not share the Project database.

## Endpoints

Base path: `/api/v1/devices/management/projects/{projectId}`.

- `GET|POST /groups`, `GET|PUT|DELETE /groups/{groupId}`
- `GET /groups/{groupId}/devices`
- `POST /groups/{groupId}/devices` with `{ "deviceIds": ["uuid"] }`
- `DELETE /groups/{groupId}/devices/{deviceId}`
- `GET|POST /tags`, `PUT|DELETE /tags/{tagId}`
- `GET|PUT /devices/{deviceId}/tags`; PUT replaces the device's organisation-tag set
- `DELETE /devices/{deviceId}/tags/{tagId}`

Names are trimmed, internal whitespace collapsed and compared case-insensitively inside a project. Duplicate names and deletion of populated groups return `409`. Invalid payloads return `400`; authentication/role/project-scope failures return `401`/`403`.

The existing `GET /api/v1/devices/inventory` accepts optional `projectId`, `groupId`, and repeated `tagIds`, in addition to search, pagination and sorting. Multiple tag values use AND semantics. A group or tag filter requires `projectId`.

Roles: `ADMIN`, `OPERATOR`, and `PROJECT_ADMIN` may manage organisation metadata, subject to Project Service access. `VIEWER` cannot use management endpoints. Existing V1 routes remain unchanged.
