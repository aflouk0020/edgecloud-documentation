# Sprint 9 Device Inventory API

## Endpoint

`GET /api/v1/devices/inventory`

The API Gateway forwards the complete path suffix and query string to Device Service. A valid EdgeCloud bearer token is required. Platform `ADMIN` and `OPERATOR` roles may read the global operational inventory; `VIEWER` is denied with 403.

| Parameter | Default | Validation |
|---|---:|---|
| `search` | empty | Case-insensitive device-name match or exact UUID |
| `page` | `0` | Zero-based, at least zero |
| `size` | `20` | 1–100 |
| `sort` | `name` | `name`, `status`, `lastSeen`, `registrationDate` |
| `direction` | `asc` | `asc` or `desc` |

The stable response contains `devices`, `page`, `size`, `totalElements`, `totalPages`, `sort` and `direction`. Each device contains its ID, name, type, stored operational status, derived heartbeat status, latest heartbeat, registration date and last-seen time. Offline devices are deliberately retained.

Repository pagination and sorting execute in MySQL. Name search is case-insensitive; a valid UUID uses an exact indexed identifier predicate. A deterministic ID tie-breaker stabilises page ordering.

## Security and errors

- Missing or invalid JWT: 401.
- Authenticated role outside `ADMIN`/`OPERATOR`: 403.
- Invalid page, size, sort or direction: 400 with a safe validation message.
- The endpoint is read-only and exposes no mutation, command, firmware or maintenance operation.

## Metadata limitations

The current Device Service schema has no firmware-version, tags or location columns. Project assignment is owned by Project Service rather than the global Device Service record. These fields are therefore returned as `null` or an empty tag list and displayed as unavailable; no synthetic data or schema-only fields were invented.
