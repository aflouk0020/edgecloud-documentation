
## Alert Types

The Alert Service classifies incidents using predefined alert types.

Supported alert types include:

- SERVICE_DOWN
- HIGH_LATENCY
- DEVICE_OFFLINE
- DATABASE_FAILURE
- CONTAINER_FAILURE

These categories allow the monitoring platform to identify the source of an operational incident and present meaningful information within the React dashboard.

---

## Severity Model

Every alert is assigned a severity level.

Supported severity levels:

- LOW
- MEDIUM
- HIGH

Typical mappings used within the platform include:

| Condition | Severity |
|-----------|----------|
| Service Down | HIGH |
| Device Offline | HIGH |
| Database Failure | HIGH |
| High Latency | MEDIUM |
| Minor Warning | LOW |

Severity values are displayed as coloured badges within the dashboard to help operators prioritise incidents.

---

## Alert Service Endpoints

The Alert Service exposes the following REST endpoints through the API Gateway.

| Method | Endpoint | Purpose |
|---------|----------|---------|
| POST | /api/v1/alerts | Create a new alert |
| GET | /api/v1/alerts | Retrieve active alerts |
| PUT | /api/v1/alerts/{id}/resolve | Resolve an alert |


## Alert Creation Workflow

A new alert is created whenever a monitored event requires operator attention.

API Endpoint:

POST /api/v1/alerts

Typical workflow:

1. A monitoring component detects an operational issue.
2. The Alert Service receives the request.
3. Request validation is performed.
4. A new alert record is stored in alert_db.
5. The created alert is returned to the client.
6. The alert immediately becomes visible on the React dashboard.

Typical stored information includes:

- Alert Type
- Severity
- Message
- Source Service
- Status
- Created Timestamp

---

## Active Alert Retrieval

API Endpoint:

GET /api/v1/alerts

This endpoint returns all unresolved active alerts.

Returned information includes:

- Alert ID
- Alert Type
- Severity
- Message
- Source Service
- Status
- Created Timestamp

Resolved alerts are automatically excluded from this endpoint so that only current operational incidents are displayed within the dashboard.


## Alert Resolution Workflow

API Endpoint:

PUT /api/v1/alerts/{id}/resolve

The Alert Service supports a simple incident lifecycle by allowing active alerts to be resolved after an issue has been investigated or corrected.

Resolution workflow:

1. The operator identifies an active alert.
2. A resolve request is submitted using the alert identifier.
3. The Alert Service locates the alert record.
4. The alert status is updated from ACTIVE to RESOLVED.
5. The resolved flag is set to true.
6. A resolved timestamp is recorded.
7. The alert is automatically removed from the active alerts endpoint.

This workflow ensures that only current operational incidents are displayed within the dashboard.

---

## Incident Lifecycle

The lifecycle implemented by the Alert Service is:

Detected

↓

Alert Created

↓

Active Alert

↓

Operator Review

↓

Resolved

↓

Removed From Active Alerts


## Rule-Based Alert Generation

The Alert Service includes simple rule-based alert generation for the MVP implementation.

Implemented rules include:

### Service Down

Condition:

A monitored service reports a status of DOWN.

Generated alert:

- Alert Type: SERVICE_DOWN
- Severity: HIGH

---

### High Latency

Condition:

A monitored service exceeds the configured response time threshold.

Generated alert:

- Alert Type: HIGH_LATENCY
- Severity: MEDIUM

---

### Device Offline

Condition:

A registered edge device reports an OFFLINE status.

Generated alert:

- Alert Type: DEVICE_OFFLINE
- Severity: HIGH

---

## Duplicate Alert Prevention

Before creating a new alert, the service checks for an existing unresolved alert representing the same incident.

If an active alert already exists, duplicate alerts are avoided where possible. This prevents unnecessary alert flooding and keeps the dashboard focused on meaningful operational issues.


## Dashboard Integration

The React dashboard communicates with the Alert Service through the API Gateway.

Current dashboard functionality includes:

- Active alert retrieval
- Severity badges
- Alert metadata display
- Source service display
- Alert resolution
- Manual refresh
- Loading state
- Empty state
- Error handling

---

## Evidence

The following evidence has been collected during Sprint 3:

- Alert creation API responses
- Active alert retrieval responses
- Alert resolution responses
- Rule-based alert generation responses
- API Gateway validation
- MySQL alert_db verification
- Docker Compose validation
- Eureka registration
- React dashboard screenshots

---

## Conclusion

The Alert Service provides the operational incident management capability for EdgeCloud Monitor.

It supports alert creation, retrieval, resolution, severity classification, and automated rule-based alert generation while integrating with Docker, Eureka, the API Gateway, MySQL, and the React dashboard.

The implementation satisfies the Sprint 3 requirements and provides a stable foundation for future monitoring enhancements.

