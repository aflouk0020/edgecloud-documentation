# SCRUM-696 Service Health Overview Evidence

## 1. Overview

SCRUM-696 delivered the Service Health Overview for EdgeCloud Monitor Version 2.0.

The implementation is intentionally project-scoped and safety-first. The Project Service owns access control and service association context, while the Monitoring Service remains the downstream authority for service identity, availability, response time, and monitoring freshness.

No global service list is treated as project-scoped data.

---

## 2. Public Project Service Endpoint

### Endpoint

```http
GET /api/v2/projects/{projectId}/service-health
```

### Response contract

The response includes:

* `projectId`
* `generatedAt`
* `totalServices`
* `healthyCount`
* `degradedCount`
* `unavailableCount`
* `unknownCount`
* `dataCompleteness`
* `services`

### Per-service record

* `serviceId`
* `serviceName`
* `serviceUrl`
* `currentHealthStatus`
* `availabilityPercentage`
* `latestMonitoringTimestamp`
* `averageResponseTime`
* `lastUpdatedAt`
* `dataState`

---

## 3. Internal Monitoring Service Endpoint

### Endpoint

```http
POST /internal/service-health
```

### Request contract

* `serviceIds`

### Response contract

* `generatedAt`
* `services`

The Monitoring Service returns only records that match the supplied service IDs.

---

## 4. Project Isolation Flow

1. The dashboard loads workspace context from the Project Service.
2. The Project Service validates project access using the authenticated caller.
3. The Project Service resolves active associated service IDs only.
4. The Project Service requests service health from the Monitoring Service using those IDs.
5. The dashboard renders only the secured response returned by the Project Service.

### Safety rules

* project access is enforced before any downstream request
* inactive associations are excluded
* archived projects remain readable
* no project aggregation endpoint is used
* no global service fallback is used
* downstream failures do not expose internal exceptions

---

## 5. Health Mapping Rules

The implementation uses a conservative mapping:

* `HEALTHY` when all resolved services are operational and availability is acceptable
* `DEGRADED` when a service is reachable but unhealthy, slow, or partially available
* `UNAVAILABLE` when a service is known but no current operational data can be resolved
* `UNKNOWN` when insufficient data exists to classify safely

### Summary counts

The overview counts:

* healthy services
* degraded services
* unavailable services
* unknown services

### Data completeness

* `COMPLETE` when all requested service-health enrichment resolves successfully
* `PARTIAL` when some requested service-health enrichment fails
* `NO_DATA` when no safe service-health data is available

---

## 6. UI Behaviour

The dashboard Service Health Overview page displays:

* summary counts
* generated timestamp
* sortable service list
* service URL where available
* latest monitoring update
* average response time
* responsive table/card layout

### UI states

* loading
* background refresh
* empty project
* API error
* unauthorised
* archived
* COMPLETE
* PARTIAL
* NO_DATA
* unavailable individual service

### Refresh behaviour

* manual Refresh Services action
* automatic refresh every 60 seconds
* duplicate concurrent requests are prevented
* polling is cleaned up on unmount

---

## 7. Known Exclusions

SCRUM-696 does not implement:

* alerts
* incidents
* topology
* dependency visualisation
* AI
* predictive scoring
* remediation
* project aggregation

---

## 8. Final Validation Results

### Backend

* Monitoring Service: `mvn clean test`, `mvn clean package`
* Project Service: `mvn clean test`, `mvn clean package`

### Frontend

* Dashboard: `npm test`, `npm run build`

### Behaviour verified

* authenticated project service-health access
* cross-project access returns `403`
* missing authentication returns `401`
* only active associated service IDs are queried
* inactive associations are excluded
* all project services are displayed
* HEALTHY / DEGRADED / UNAVAILABLE / UNKNOWN states render correctly
* availability percentage and average response time render correctly
* latest monitoring update renders correctly
* deterministic service-name sorting works
* empty projects render safely
* archived projects remain readable
* PARTIAL and NO_DATA states render safely
* one unavailable service does not fail the full overview
* manual refresh works
* 60-second automatic refresh works
* duplicate concurrent refreshes are prevented
* polling is cleaned up on unmount
* no service-health request occurs before workspace access succeeds
* responsive table/card layout remains readable
* Version 1.0 dashboard routes remain operational

