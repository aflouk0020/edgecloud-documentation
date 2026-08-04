# SCRUM-697 Edge Device Health Overview Evidence

## 1. Story Purpose and Scope

SCRUM-697 delivers the Edge Device Health Overview for EdgeCloud Monitor Version 2.0.

The feature is project-scoped and safety-first:

- the Project Service owns project access and active device associations
- the Device Service owns device identity, status, and latest heartbeat
- the Monitoring Service owns telemetry freshness
- no global device list is treated as project-scoped data

The dashboard renders only the secured Project Service response and never uses client-side filtering to enforce isolation.

---

## 2. Public Project Service Endpoint

### Endpoint

```http
GET /api/v2/projects/{projectId}/device-health
```

### Response contract

Overview:

- `projectId`
- `generatedAt`
- `totalDevices`
- `onlineCount`
- `offlineCount`
- `degradedCount`
- `unavailableCount`
- `unknownCount`
- `dataCompleteness`
- `devices`

Per-device record:

- `deviceId`
- `deviceName`
- `deviceType`
- `ipAddress`
- `currentStatus`
- `healthStatus`
- `availability`
- `latestHeartbeat`
- `latestTelemetryReceivedAt`
- `lastUpdatedAt`
- `dataState`

---

## 3. Internal Device Service Endpoint

### Endpoint

```http
POST /internal/device-health
```

### Request contract

- `deviceIds`

### Response contract

- `generatedAt`
- `devices`

The Device Service returns only records that match the supplied device IDs.

---

## 4. Internal Monitoring Service Endpoint

### Endpoint

```http
POST /internal/device-telemetry-health
```

### Request contract

- `deviceIds`

### Response contract

- `generatedAt`
- `devices`

The Monitoring Service returns only telemetry freshness records for the supplied device IDs.

---

## 5. Project Isolation Flow

1. The dashboard loads workspace context from the Project Service.
2. The Project Service validates project access using the authenticated caller.
3. The Project Service resolves active associated device IDs only.
4. The Project Service requests device identity/status from the Device Service using those IDs.
5. The Project Service requests telemetry freshness from the Monitoring Service using the same IDs.
6. The dashboard renders only the secured response returned by the Project Service.

### Safety rules

- access is validated before any downstream request
- inactive associations are excluded
- archived projects remain readable
- no global device fallback is used
- downstream failures do not expose internal exceptions
- no project aggregation endpoint is used

---

## 6. Active Device-Association Filtering

Only active project-device associations are used.

Inactive associations are excluded from downstream calls and from the rendered overview.

This keeps the overview aligned with the current project membership context and prevents cross-project leakage.

---

## 7. Device Identity and Status Source

The Device Service is the source of truth for:

- device name
- device type
- IP address
- current status
- health status
- latest heartbeat

The Project Service does not invent device identity or status values.

---

## 8. Existing Heartbeat Threshold Behaviour

The Device Service continues to apply its existing heartbeat threshold logic when evaluating whether a device should be marked offline.

That threshold behaviour is reused as-is and is not redefined by the Project Service.

---

## 9. Telemetry Freshness Source

The Monitoring Service is the source of truth for:

- latest telemetry received timestamp
- telemetry freshness state used by the overview

The Project Service only forwards associated device IDs and merges the safe response.

---

## 10. Device-Health Mapping Rules

The overview uses conservative mapping:

- `HEALTHY` when the device is operational and telemetry freshness is acceptable
- `DEGRADED` when the device is reachable but unhealthy, slow, or partially available
- `OFFLINE` when the device is known to be offline
- `UNAVAILABLE` when the device is associated but no safe operational data can be resolved
- `UNKNOWN` when the available data is insufficient to classify safely

### Data completeness

- `COMPLETE` when all associated device-health enrichment resolves successfully
- `PARTIAL` when some device-health enrichment fails
- `NO_DATA` when no safe device-health data is available

### Counts

The overview reports:

- total devices
- online count
- offline count
- degraded count
- unavailable count
- unknown count

---

## 11. Partial and Complete Downstream Failure Handling

- A single downstream failure does not fail the full overview.
- Partially resolved devices are returned with safe fallback values.
- Complete downstream failure returns a safe summary with unavailable device records where possible.
- No downstream exception details are exposed to the client.

---

## 12. Deterministic Sorting

The final overview sorts devices deterministically by:

1. device name ascending, case-insensitive
2. device ID as the fallback tie-breaker

This keeps the list stable across refreshes and repeated requests.

---

## 13. Dashboard Route

```http
/projects/:projectId/devices
```

The route is connected to the existing project-centred navigation and reuses the workspace context load-before-enrichment pattern.

---

## 14. Refresh Behaviour

The dashboard supports:

- manual Refresh Devices action
- automatic refresh every 60 seconds
- duplicate concurrent request protection
- polling cleanup on unmount

The page preserves the current data during background refresh.

---

## 15. Responsive UI Layout

The overview uses a responsive table-to-card layout so it remains usable on:

- desktop
- tablet
- mobile

It also preserves clear labels for:

- latest heartbeat
- latest telemetry received
- health status
- data state

---

## 16. Known Limitations

- availability remains unavailable unless backed by a real source
- no device-management features are included
- no remote-action, firmware, diagnostics, or predictive maintenance features are included

---

## 17. Final Build and Test Results

- Device Service: 19 tests passed
- Monitoring Service: 53 tests passed
- Project Service: 163 tests passed
- Dashboard: 77 tests passed

---

## 18. Evidence Checklist

### Captured in code and validation

- API response contract
- healthy device behaviour
- degraded device behaviour
- offline device behaviour
- unavailable device behaviour
- empty project handling
- partial-data state
- 401 and 403 validation
- backend and frontend test results

### Pending evidence

The following screenshots / visual captures were not produced during this closure pass and remain pending:

- desktop layout
- tablet layout
- mobile layout

