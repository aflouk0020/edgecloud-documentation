# SCRUM-693 Project Health Summary Evidence

## 1. Overview

SCRUM-693 delivered the first lightweight, project-centred operational dashboard for EdgeCloud Monitor Version 2.0.

The implementation is intentionally limited to safe operational summary data. It does not introduce historical charts, alerts, analytics, reports, or project aggregation.

The Project Service remains the source of truth for project access and workspace context. Monitoring and Device Services remain the downstream authorities for telemetry and device state.

---

## 2. Health Summary API

### Endpoint

```http
GET /api/v2/projects/{projectId}/health-summary
```

### Response contract

The response includes:

* `projectId`
* `projectName`
* `projectStatus`
* `overallHealth`
* `totalRegisteredDevices`
* `onlineDevices`
* `offlineDevices`
* `activeMonitoringServices`
* `latestTelemetryReceivedAt`
* `monitoringStatus`
* `generatedAt`
* `dataCompleteness`

### Health values

* `overallHealth`: `HEALTHY`, `DEGRADED`, `CRITICAL`, `UNKNOWN`
* `monitoringStatus`: `AVAILABLE`, `PARTIAL`, `UNAVAILABLE`
* `dataCompleteness`: `COMPLETE`, `PARTIAL`, `NO_DATA`

---

## 3. Downstream Interaction Model

The Project Service coordinates enrichment safely using only identifiers associated with the selected project.

### Monitoring Service

Used for:

* monitored service detail lookup
* service availability / status
* latest telemetry timestamp where available

### Device Service

Used for:

* registered device detail lookup
* online / offline status
* last heartbeat where available

### Safety rules

* no global telemetry collection is treated as project-scoped data
* no project aggregation endpoint is called
* only associated IDs are requested downstream
* one downstream failure does not fail the full summary
* downstream exceptions are not exposed to the UI

---

## 4. Health Calculation Rules

The summary uses a conservative, explainable rule set:

* `HEALTHY` when all resolved services are active and all resolved devices are online
* `DEGRADED` when at least one associated resource is unhealthy, offline, or unavailable
* `CRITICAL` when there are no active services or all resolved devices are offline where resources exist
* `UNKNOWN` when operational data is insufficient

### Data completeness

* `COMPLETE` when all requested enrichment resolves successfully
* `PARTIAL` when some requested enrichment fails
* `NO_DATA` when no operational enrichment is available

### Telemetry fallback

If no safe telemetry timestamp is available, the UI shows:

* `No telemetry timestamp available yet`

---

## 5. Frontend Workspace Integration

The dashboard’s Project Observability Workspace page now shows:

* overall project health
* total registered devices
* online devices
* offline devices
* active monitoring services
* last telemetry received
* monitoring status

### UI states

* loading
* empty
* error
* unauthorised
* archived
* partial
* unavailable enrichment

### Refresh behaviour

* manual refresh action
* automatic refresh every 60 seconds
* no duplicate concurrent refresh requests
* refresh timer cleaned up on unmount

---

## 6. Known Limitation

Project-level metric aggregation remains unsupported and continues to return `501 Not Implemented`.

This is intentional and preserves the safety boundary until project aggregation is wired to the new Project Service source of truth.

---

## 7. Testing and Validation Evidence

### Backend

Validated with:

* `mvn clean test`
* `mvn clean package`

### Frontend

Validated with:

* `npm test`
* `npm run build`

### Behaviour verified

* authenticated project health-summary access
* project-level authorisation
* cross-project rejection with `403`
* missing authentication with `401`
* overall health rendering
* device count rendering
* active monitoring service count rendering
* latest telemetry fallback
* AVAILABLE / PARTIAL / UNAVAILABLE monitoring states
* COMPLETE / PARTIAL / NO_DATA states
* archived project visibility
* partial downstream failure handling
* manual refresh
* automatic refresh cleanup
* no global telemetry shown as project-scoped
* Version 1.0 dashboard routes remain operational

