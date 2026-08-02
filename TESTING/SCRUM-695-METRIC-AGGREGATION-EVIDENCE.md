# SCRUM-695 Metric Aggregation Evidence

## 1. Overview

SCRUM-695 delivered the metric aggregation workflow for EdgeCloud Monitor across the Monitoring Service and Dashboard.

The implementation was intentionally limited to service-level and device-level aggregation in the live UI. Project aggregation remains unavailable because the Monitoring Service does not yet have authoritative project ownership metadata.

---

## 2. Aggregation API Endpoints

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

## 6. Validation Evidence

### Backend

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
