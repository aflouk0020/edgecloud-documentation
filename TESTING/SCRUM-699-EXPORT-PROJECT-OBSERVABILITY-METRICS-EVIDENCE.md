# SCRUM-699 Export Project Observability Metrics Evidence

## 1. Scope

SCRUM-699 delivered CSV export for project historical metrics in EdgeCloud Monitor Version 2.0.

The feature is intentionally project-scoped and safety-first. Export is only available after the Project Service has validated project access, and the export result is generated from the bounded historical metrics dataset already resolved for that project context.

This supports:

- operational evidence collection
- incident investigation
- audit support
- external analysis

The implementation does not introduce new monitoring persistence, does not use global telemetry as project-scoped data, and does not weaken project isolation.

---

## 2. Architecture

The export flow is:

Dashboard
↓
Project Service authorization
↓
Monitoring Service historical query
↓
CSV generation
↓
Browser download

### Responsibilities

- React Dashboard: presents the Export CSV action and initiates the download
- API Gateway: forwards the secured project export request
- Project Service: validates project access and coordinates the bounded export request
- Monitoring Service: provides the historical metric data used to generate the CSV

---

## 3. API Contract

### Public Project Service endpoint

```http
GET /api/v2/projects/{projectId}/metrics/export
```

Query parameters:

- `from`
- `to`
- `metricTypes`
- `deviceId`
- `serviceId`
- `sortDirection`

### Response

- `Content-Type: text/csv; charset=UTF-8`
- `Content-Disposition: attachment; filename="<safe-generated-filename>"`
- CSV payload returned as a browser download

The browser uses the backend-provided filename when present and falls back safely when it is not.

---

## 4. Security

The export workflow enforces:

- authenticated users only
- project authorization
- archived project support
- no cross-project export
- bounded export size
- date-range validation
- CSV formula-injection protection
- filename sanitization
- no global telemetry fallback

Project-scoped export is only allowed after Project Service access checks succeed.

---

## 5. CSV Structure

Exported columns:

- `project_id`
- `project_name`
- `metric_type`
- `metric_value`
- `unit`
- `source_type`
- `source_id`
- `device_id`
- `service_id`
- `recorded_at`

This structure is stable for the current release. Future versions may extend the export without breaking compatibility.

---

## 6. Frontend Behaviour

The dashboard Historical Metrics Explorer includes:

- Export CSV button
- reuse of the currently selected filters
- loading state
- duplicate request prevention
- download initiation
- filename handling
- fallback filename
- export success feedback
- validation failure feedback
- empty export feedback
- unauthorized export feedback
- generic failure feedback

The browser download is initiated with an object URL and a temporary anchor. The page state remains unchanged during export.

---

## 7. Validation Summary

### Backend

- 199 backend tests passed

### Frontend

- 99 frontend tests passed

### Builds

- Maven build passed
- Vite build passed

---

## 8. Evidence Checklist

### Already documented in this evidence set

- API contract
- security model
- CSV structure
- frontend export behaviour
- build and test results

### Pending manual capture

- Historical Metrics page
- Export button
- Successful download
- CSV opened in spreadsheet
- Validation error
- Empty export
- Unauthorized export

Status: PENDING MANUAL CAPTURE

---

## 9. Known Exclusions

SCRUM-699 intentionally excludes:

- PDF export
- scheduled export
- email delivery
- background export jobs
- OpenAPI documentation updates
- any change to metric aggregation behavior

---

## 10. Dependency Note

SCRUM-699 depends on the historical metrics foundation established in SCRUM-694 and the shared observability workspace and polling work delivered in SCRUM-692 through SCRUM-698.

