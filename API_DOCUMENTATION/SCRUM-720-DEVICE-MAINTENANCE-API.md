# SCRUM-720 Device Maintenance API

## Purpose

Device maintenance mode records intentional device unavailability without deactivating or deleting the device. Browser-facing requests use API Gateway and the existing bearer JWT flow; the Dashboard does not call Device Service directly.

## Global endpoints

| Method | Gateway path | Purpose |
|---|---|---|
| `GET` | `/api/v1/devices/management/{deviceId}/maintenance` | Retrieve current maintenance state |
| `POST` | `/api/v1/devices/management/{deviceId}/maintenance` | Enable maintenance |
| `DELETE` | `/api/v1/devices/management/{deviceId}/maintenance` | Disable maintenance |
| `GET` | `/api/v1/devices/management/{deviceId}/maintenance/history` | Retrieve newest-first durable history |

## Project-scoped endpoints

The same operations are exposed beneath:

```text
/api/v1/devices/management/projects/{projectId}/devices/{deviceId}/maintenance
/api/v1/devices/management/projects/{projectId}/devices/{deviceId}/maintenance/history
```

Device Service asks Project Service to verify that the device belongs to the supplied project before reading or mutating maintenance state.

## Enable contract

```json
{
  "reason": "Planned hardware inspection",
  "scheduledEndAt": "2026-08-17T10:00:00"
}
```

Both fields are optional. `reason` is limited to 500 characters. A supplied end must be in the future. There is no scheduled future start.

An exact repeated enable with the same normalized reason and end is idempotent and returns `200` without another history event. Enabling an already-maintained device with different values returns `409`. Repeated disable is an idempotent `204`.

## State response

The current-state response includes `deviceId`, `maintenanceMode`, reason, enabled timestamp/actor UUID, optional scheduled end, and the latest disabled timestamp/actor UUID. Inventory responses expose the active maintenance fields so the Dashboard can render state without per-row requests.

## Security and errors

| Behaviour | Result |
|---|---|
| `ADMIN` or `OPERATOR` global mutation | Permitted |
| `PROJECT_ADMIN` project-scoped read | Permitted after association validation |
| `PROJECT_ADMIN` mutation | `403` |
| `VIEWER` maintenance access | `403` |
| Missing/invalid bearer token | `401` |
| Invalid reason/end | `400` |
| Cross-project access | `403` |
| Missing device | `404` |
| Inactive-device enable or conflicting enable | `409` |

Inactive devices may still be read and maintenance may be disabled. A deleted device has no current state (`404`), while its retained history remains readable when history exists.
