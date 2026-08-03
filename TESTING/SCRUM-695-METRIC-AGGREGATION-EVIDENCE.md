# SCRUM-695 Metric Aggregation Evidence

## Project Service Foundation Closure Note

The Project Service foundation is now in place as the production-safe organisational layer for EdgeCloud Monitor Version 2.0.

This closure document records the supporting platform work that made SCRUM-695 possible and that will act as the prerequisite foundation for SCRUM-692.

## 1. Overview

SCRUM-695 delivered the metric aggregation workflow for EdgeCloud Monitor across the Monitoring Service and Dashboard.

The implementation was intentionally limited to service-level and device-level aggregation in the live UI. Project aggregation remains unavailable because the Monitoring Service does not yet have authoritative project ownership metadata.

The broader platform foundation now includes:

* a dedicated Project Service
* project, membership, service-association, and device-association domain models
* JWT-protected project-level authorisation
* API Gateway routing for `/api/v2/projects/**`
* dedicated project database support and Flyway schema management
* Eureka registration and health checks
* Docker Compose integration for local orchestration

---

## 2. Project Service Architecture

### Service boundary

The Project Service owns the following logical responsibilities:

* project lifecycle
* membership and access control
* logical service associations
* logical device associations

The service does not own monitored telemetry or device records. It stores logical identifiers only and avoids cross-service foreign keys.

### Domain model

* `Project`
  * UUID identifier
  * name
  * description
  * status
  * ownerUserId
  * createdAt
  * updatedAt
* `ProjectMember`
  * projectId
  * userId
  * project role
  * active status
* `ProjectServiceAssociation`
  * projectId
  * serviceId
  * active status
* `ProjectDeviceAssociation`
  * projectId
  * deviceId
  * active status

### Authorisation rules

The Project Service reuses the existing EdgeCloud JWT contract and enforces access by authenticated caller identity and role.

* `ADMIN`
  * manage all projects
  * manage memberships and associations
* `PROJECT_ADMIN`
  * manage only projects where they have active `PROJECT_ADMIN` membership
* `OPERATOR`
  * read access to allowed project views
* `VIEWER`
  * read-only access
* inactive members
  * no access

Archived projects remain retrievable but reject normal updates and new associations.

### API endpoints

```http
POST   /api/v2/projects
GET    /api/v2/projects
GET    /api/v2/projects/{projectId}
PUT    /api/v2/projects/{projectId}
POST   /api/v2/projects/{projectId}/archive
GET    /api/v2/projects/{projectId}/access
GET    /api/v2/projects/{projectId}/members
POST   /api/v2/projects/{projectId}/members
PUT    /api/v2/projects/{projectId}/members/{userId}
DELETE /api/v2/projects/{projectId}/members/{userId}
POST   /api/v2/projects/{projectId}/members/{userId}/reactivate
POST   /api/v2/projects/{projectId}/services
GET    /api/v2/projects/{projectId}/services
DELETE /api/v2/projects/{projectId}/services/{serviceId}
POST   /api/v2/projects/{projectId}/services/{serviceId}/reactivate
POST   /api/v2/projects/{projectId}/devices
GET    /api/v2/projects/{projectId}/devices
DELETE /api/v2/projects/{projectId}/devices/{deviceId}
POST   /api/v2/projects/{projectId}/devices/{deviceId}/reactivate
```

### JWT integration

The Project Service authenticates requests using the existing EdgeCloud JWT contract. The gateway forwards protected requests, and the service validates the token, extracts the caller user ID and platform role, and enforces project-level authorisation in the backend.

### Gateway routing

The API Gateway now routes `/api/v2/projects/**` to `edgecloud-project-service` while preserving the full path.

### Docker Compose integration

The local orchestration layer now includes:

* `edgecloud-project-service`
* `edgecloud-project-db`

### Eureka and health

The service registers with Eureka on startup and exposes Actuator health checks for deployment validation.

### Flyway and database design

The Project Service uses its own MySQL database and Flyway-managed schema migrations. The model intentionally stores only logical references for users, services, and devices.

### Known limitations

* project observability aggregation remains unavailable until real project ownership is added
* service and device associations are logical links only; external existence validation is a later integration step
* project aggregation in monitoring remains `501 Not Implemented` for now

### Dependency relationship with SCRUM-692

SCRUM-692 depends on this Project Service foundation. It can now build the observability workspace on top of a real project source of truth instead of relying on temporary or global aggregates.

---

## 3. Aggregation API Endpoints

### Monitoring Service

```http
GET /aggregation/projects/{projectId}
GET /aggregation/services/{serviceId}
GET /aggregation/devices/{deviceId}
```

### Dashboard Integration

The dashboard consumes:

* service aggregation for the Services view
* device aggregation for the Devices view

The dashboard does not call the project aggregation endpoint.

---

## 3. Supported Metrics

The aggregation contract returns structured summary data for:

* average value
* minimum value
* maximum value
* latest value
* sample count
* total telemetry received
* latest telemetry timestamp
* average response time
* service availability
* device availability

The response also includes:

* aggregation scope
* date-range metadata
* empty-result handling
* per-record series points for charting or future UI expansion

---

## 4. Date-Range Rules

Validation rules enforced by the API:

* optional ISO-8601 `from` and `to` query parameters
* `from` must not be after `to`
* ranges longer than 90 days are rejected
* malformed timestamps are rejected with a bad request response

Open-ended requests are allowed when one or both dates are omitted.

---

## 5. Architecture and Calculation Approach

The aggregation feature reuses the existing telemetry and service metric entities.

Implementation characteristics:

* repository queries fetch the relevant records by scope and date range
* aggregation logic is performed in the service layer
* results are deterministic for identical inputs
* empty datasets return an explicit empty-result response
* project-level aggregation is represented as `501 Not Implemented`

This approach keeps the feature small, maintainable, and aligned with the existing monitoring architecture.

---

## 6. Live Smoke-Test Evidence

Validated live with:

* Discovery Service started successfully
* Project Service registered with Eureka
* API Gateway registered successfully
* Project Service health endpoint reported `UP`
* unauthenticated Gateway request returned `401`
* authenticated request with valid JWT reached Project Service
* project creation and retrieval through the Gateway
* automatic owner membership creation
* service association creation and retrieval
* device association creation and retrieval
* cross-project access rejection
* archived project access rejection
* archived project association rejection
* no visible impact to existing EdgeCloud services

### Backend test evidence

Validated with:

* `mvn clean test`
* `mvn clean package`

Coverage included:

* successful service aggregation
* successful device aggregation
* date-range validation
* empty-result handling
* project aggregation returning 501
* controller and service test coverage

### Gateway test evidence

Validated with:

* `mvn clean test`

Coverage included:

* project route authentication enforcement
* `/api/v2/projects/**` routing integration

### Frontend

Validated with:

* `npm test`
* `npm run build`

Coverage included:

* service aggregation rendering
* device aggregation rendering
* loading states
* empty states
* error states
* project aggregation unavailable messaging

---

## 7. Outcome

SCRUM-695 adds the first production-ready metric aggregation workflow for EdgeCloud Monitor without introducing new tables or changing project aggregation behavior. The result is consistent with the existing monitoring stack and ready for future expansion once project ownership data becomes available.
