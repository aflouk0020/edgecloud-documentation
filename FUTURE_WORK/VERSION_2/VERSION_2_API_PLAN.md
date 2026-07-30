# EdgeCloud Platform Version 2.0 API Plan

## 1. Purpose

This document defines the API planning approach for EdgeCloud Platform Version 2.0.

It establishes:

- API design principles
- Resource naming
- Versioning
- Authentication
- Authorisation
- Error handling
- Pagination
- Filtering
- Idempotency
- Webhook handling
- Documentation expectations
- Compatibility with Version 1.0

The objective is to create predictable, secure and maintainable service interfaces.

---

## 2. Core API Principles

Version 2.0 APIs must be:

- Versioned
- Resource-oriented
- Secure
- Consistent
- Validated
- Documented
- Testable
- Backwards-compatible where required
- Suitable for frontend and service-to-service use

Controllers should remain thin.

Business rules must remain in service layers.

---

## 3. API Versioning

New Version 2.0 endpoints should use:

`/api/v2`

Examples:

`/api/v2/projects`

`/api/v2/projects/{projectId}`

`/api/v2/projects/{projectId}/devices`

Existing Version 1.0 endpoints should remain available until a documented migration is complete.

Breaking changes must not be introduced silently.

---

## 4. Resource Naming

API paths should use:

- Lowercase names
- Plural resource names
- Hyphenated multi-word names
- Stable identifiers
- Clear parent-child relationships

Examples:

`/api/v2/projects`

`/api/v2/build-executions`

`/api/v2/quality-findings`

`/api/v2/organisations/{organisationId}/members`

Avoid action-style paths unless the operation does not map naturally to standard HTTP methods.

---

## 5. HTTP Method Standards

| Method | Purpose |
| --- | --- |
| GET | Retrieve resources |
| POST | Create a resource or trigger a non-idempotent operation |
| PUT | Replace a complete resource |
| PATCH | Update selected fields |
| DELETE | Remove or deactivate a resource |

Operations should use the most appropriate HTTP method.

---

## 6. HTTP Status Codes

Recommended responses include:

| Status | Meaning |
| --- | --- |
| 200 | Successful retrieval or update |
| 201 | Resource created |
| 202 | Asynchronous request accepted |
| 204 | Successful request with no response body |
| 400 | Invalid request |
| 401 | Authentication required or invalid |
| 403 | Authenticated but not authorised |
| 404 | Resource not found |
| 409 | Conflict or duplicate state |
| 422 | Valid request format but unacceptable business state |
| 429 | Rate limit exceeded |
| 500 | Unexpected internal error |
| 503 | Service temporarily unavailable |

Status codes must reflect the actual outcome.

---

## 7. Authentication

Protected APIs must require a valid authentication token.

Authentication responsibilities include:

- Token validation
- Expiry validation
- Signature validation
- User identity extraction
- Role extraction
- Safe failure responses

Authentication should be handled consistently through the platform security architecture.

---

## 8. Authorisation

Authorisation must consider:

- User role
- Project membership
- Project role
- Organisation membership
- Organisation role
- Resource ownership
- Administrative permission

Authorisation must be enforced in backend services.

Frontend visibility rules do not replace backend checks.

---

## 9. Request Validation

Requests should validate:

- Required fields
- Field lengths
- Supported values
- Numeric ranges
- Identifier formats
- Date and time formats
- Ownership scope
- Duplicate state
- Business rules

Validation responses should identify the affected field where appropriate.

---

## 10. Response Models

Public APIs should return DTOs rather than persistence entities.

Response models should:

- Include stable field names
- Exclude internal database details
- Exclude secrets
- Avoid exposing unnecessary relationships
- Use consistent timestamp formats
- Use consistent identifier formats

Nested objects should be limited to useful and controlled information.

---

## 11. Error Response Standard

Errors should use a consistent structure.

Suggested fields include:

| Field | Purpose |
| --- | --- |
| timestamp | Time of the error |
| status | HTTP status code |
| error | Error category |
| message | Safe user-facing explanation |
| path | Request path |
| correlationId | Trace identifier |
| validationErrors | Optional field-level errors |

Internal stack traces must not be exposed through production APIs.

---

## 12. Pagination

Large collections must support pagination.

Suggested query parameters:

- page
- size
- sort
- direction

Suggested response metadata:

- currentPage
- pageSize
- totalElements
- totalPages
- first
- last

Maximum page size should be controlled by the service.

---

## 13. Filtering and Search

APIs may support filters such as:

- status
- severity
- projectId
- organisationId
- deviceId
- serviceId
- repositoryId
- branch
- dateFrom
- dateTo
- search

Filters should be documented and validated.

Search behaviour should remain predictable.

---

## 14. Sorting

Sortable endpoints should define approved fields.

Examples include:

- createdAt
- updatedAt
- name
- status
- severity
- duration
- timestamp

Clients must not be allowed to sort using arbitrary database expressions.

---

## 15. Date and Time Standards

APIs should use ISO 8601 timestamps.

Timestamps should include timezone information.

Backend storage should normally use UTC.

Frontend applications may convert timestamps for display.

---

## 16. Idempotency

Operations that may be retried should be idempotent where possible.

Examples include:

- Device heartbeat submission
- Telemetry ingestion
- Webhook processing
- Deployment status updates
- Build result ingestion

Idempotency may use:

- Event identifiers
- Request identifiers
- Deduplication keys
- Unique constraints
- Existing-resource checks

---

## 17. Project Service API Plan

Potential Project Service endpoints include:

| Method | Endpoint | Purpose |
| --- | --- | --- |
| POST | /api/v2/projects | Create project |
| GET | /api/v2/projects | List accessible projects |
| GET | /api/v2/projects/{projectId} | Retrieve project |
| PATCH | /api/v2/projects/{projectId} | Update project |
| DELETE | /api/v2/projects/{projectId} | Archive or delete project |
| GET | /api/v2/projects/{projectId}/members | List project members |
| POST | /api/v2/projects/{projectId}/members | Add project member |
| DELETE | /api/v2/projects/{projectId}/members/{userId} | Remove project member |
| GET | /api/v2/projects/{projectId}/devices | List project devices |
| GET | /api/v2/projects/{projectId}/services | List project services |

Final endpoint scope must be confirmed through Jira stories.

---

## 18. Monitoring API Plan

Potential monitoring endpoints include:

| Method | Endpoint | Purpose |
| --- | --- | --- |
| POST | /api/v2/metrics | Ingest telemetry |
| GET | /api/v2/metrics | Query metrics |
| GET | /api/v2/projects/{projectId}/metrics | Query project metrics |
| GET | /api/v2/devices/{deviceId}/metrics | Query device metrics |
| GET | /api/v2/services/{serviceId}/metrics | Query service metrics |
| GET | /api/v2/projects/{projectId}/health | Retrieve project health summary |

High-volume metric queries must require bounded time ranges.

---

## 19. Device API Plan

Potential device endpoints include:

| Method | Endpoint | Purpose |
| --- | --- | --- |
| POST | /api/v2/devices | Register device |
| GET | /api/v2/devices | List accessible devices |
| GET | /api/v2/devices/{deviceId} | Retrieve device |
| PATCH | /api/v2/devices/{deviceId} | Update device metadata |
| POST | /api/v2/devices/{deviceId}/heartbeat | Submit heartbeat |
| GET | /api/v2/projects/{projectId}/devices | List project devices |

Device registration and heartbeat operations must be retry-safe.

---

## 20. Alert and Incident API Plan

Potential endpoints include:

| Method | Endpoint | Purpose |
| --- | --- | --- |
| GET | /api/v2/alerts | List alerts |
| GET | /api/v2/alerts/{alertId} | Retrieve alert |
| PATCH | /api/v2/alerts/{alertId}/acknowledgement | Acknowledge alert |
| PATCH | /api/v2/alerts/{alertId}/resolution | Resolve alert |
| GET | /api/v2/incidents | List incidents |
| POST | /api/v2/incidents | Create incident |
| GET | /api/v2/incidents/{incidentId} | Retrieve incident |
| PATCH | /api/v2/incidents/{incidentId} | Update incident |
| POST | /api/v2/incidents/{incidentId}/timeline | Add timeline entry |

State transitions must be validated in the service layer.

---

## 21. Integration API Plan

Potential integration endpoints include:

| Method | Endpoint | Purpose |
| --- | --- | --- |
| POST | /api/v2/integrations/github | Connect repository |
| GET | /api/v2/integrations | List integrations |
| GET | /api/v2/integrations/{integrationId} | Retrieve integration |
| DELETE | /api/v2/integrations/{integrationId} | Disconnect integration |
| POST | /api/v2/webhooks/github | Receive GitHub webhook |
| POST | /api/v2/integrations/{integrationId}/sync | Trigger synchronisation |
| GET | /api/v2/integrations/{integrationId}/health | Retrieve integration health |

Webhook endpoints must not rely on standard user authentication alone.

---

## 22. Build API Plan

Potential build endpoints include:

| Method | Endpoint | Purpose |
| --- | --- | --- |
| POST | /api/v2/builds | Start build |
| GET | /api/v2/builds | List builds |
| GET | /api/v2/builds/{buildId} | Retrieve build |
| POST | /api/v2/builds/{buildId}/cancel | Cancel build |
| GET | /api/v2/builds/{buildId}/stages | List build stages |
| GET | /api/v2/builds/{buildId}/logs | Retrieve build logs |
| GET | /api/v2/projects/{projectId}/builds | List project builds |

Build creation should return `202 Accepted` when execution is asynchronous.

---

## 23. Quality API Plan

Potential quality endpoints include:

| Method | Endpoint | Purpose |
| --- | --- | --- |
| GET | /api/v2/projects/{projectId}/quality | Retrieve quality summary |
| GET | /api/v2/test-results | List test results |
| GET | /api/v2/quality-findings | List quality findings |
| PATCH | /api/v2/quality-findings/{findingId} | Update finding state |
| GET | /api/v2/projects/{projectId}/quality/trends | Retrieve quality trends |

Quality endpoints should support filtering by branch, build and date range.

---

## 24. Analytics and Reporting API Plan

Potential endpoints include:

| Method | Endpoint | Purpose |
| --- | --- | --- |
| GET | /api/v2/projects/{projectId}/analytics | Retrieve project analytics |
| GET | /api/v2/projects/{projectId}/health-summary | Retrieve health summary |
| GET | /api/v2/projects/{projectId}/trends | Retrieve project trends |
| POST | /api/v2/reports | Generate report |
| GET | /api/v2/reports/{reportId} | Retrieve report status |
| GET | /api/v2/reports/{reportId}/download | Download generated report |

Long-running reports should be asynchronous.

---

## 25. Organisation API Plan

Potential organisation endpoints include:

| Method | Endpoint | Purpose |
| --- | --- | --- |
| POST | /api/v2/organisations | Create organisation |
| GET | /api/v2/organisations | List accessible organisations |
| GET | /api/v2/organisations/{organisationId} | Retrieve organisation |
| PATCH | /api/v2/organisations/{organisationId} | Update organisation |
| GET | /api/v2/organisations/{organisationId}/members | List members |
| POST | /api/v2/organisations/{organisationId}/members | Add member |
| DELETE | /api/v2/organisations/{organisationId}/members/{userId} | Remove member |

Organisation endpoints require strict tenant isolation.

---

## 26. Audit API Plan

Potential audit endpoints include:

| Method | Endpoint | Purpose |
| --- | --- | --- |
| GET | /api/v2/audit-events | Search authorised audit events |
| GET | /api/v2/projects/{projectId}/audit-events | Retrieve project audit history |
| GET | /api/v2/organisations/{organisationId}/audit-events | Retrieve organisation audit history |

Audit APIs must be read-only for normal clients.

Audit creation should occur within backend workflows.

---

## 27. Webhook Standards

Webhook processing must include:

- Provider identification
- Signature validation
- Timestamp validation
- Replay protection
- Event-type validation
- Idempotency
- Safe payload parsing
- Failure logging
- Retry handling
- Limited payload retention

Webhook secrets must not appear in logs.

---

## 28. Rate Limiting

Rate limiting should be considered for:

- Authentication endpoints
- Webhook endpoints
- Report generation
- Build execution
- Search-heavy APIs
- Public health endpoints
- Telemetry ingestion

Rate-limit responses should use HTTP `429`.

---

## 29. Service-to-Service Communication

Internal service calls should use:

- Stable internal APIs
- Timeouts
- Retry policies
- Correlation identifiers
- Authentication where required
- Circuit-breaking where justified
- Clear failure states

Services must not assume that another service is always available.

---

## 30. API Documentation

Every public endpoint should document:

- Purpose
- Method
- Path
- Required role
- Request fields
- Response fields
- Status codes
- Validation rules
- Example request
- Example response
- Error responses

OpenAPI documentation should be generated and reviewed.

---

## 31. API Testing

API testing should include:

- Success cases
- Validation failures
- Authentication failures
- Authorisation failures
- Not-found cases
- Conflict cases
- Pagination
- Filtering
- Sorting
- Idempotency
- Cross-project access
- Cross-tenant access
- Webhook verification

Tests must directly reflect Jira acceptance criteria.

---

## 32. Compatibility and Deprecation

Deprecated endpoints should:

- Remain available for a defined transition period
- Be documented as deprecated
- Provide replacement guidance
- Be monitored for remaining use
- Be removed only through an approved release decision

Breaking changes require explicit versioning.

---

## 33. API Review Checklist

Before implementing or changing an API, confirm:

- The owning service is clear.
- The endpoint follows naming standards.
- The correct HTTP method is used.
- Authentication is defined.
- Authorisation is defined.
- Validation is defined.
- Status codes are correct.
- Error handling is consistent.
- Pagination is added where required.
- Idempotency is considered.
- Tests are planned.
- OpenAPI documentation will be updated.
- Version 1.0 compatibility is protected.

---

## 34. Current Status

**Status:** Draft

**Owner:** Taha Aflouk

**Version:** EdgeCloud Platform Version 2.0

**Previous document:** VERSION_2_DATABASE_PLAN.md

**Next document:** VERSION_2_UI_UX_PLAN.md
