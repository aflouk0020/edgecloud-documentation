# SCRUM-694 Historical Metrics Explorer Evidence

## 1. Scope

SCRUM-694 delivered the first secure Historical Metrics Explorer for EdgeCloud Monitor Version 2.0.

The implementation is intentionally scoped to project-associated telemetry only. It does not use metric aggregation, does not fall back to global telemetry, and preserves project isolation through the Project Service source of truth.

---

## 2. API Contract

### Project Service

```http
GET /api/v2/projects/{projectId}/historical-metrics
```

Query parameters:

- `from`
- `to`
- `page`
- `size`
- `sortDirection`

### Monitoring Service internal query

Project Service forwards only project-associated service IDs and device IDs to Monitoring Service.

The internal query contract supports:

- allowed service IDs
- allowed device IDs
- date range
- page
- size
- sort direction

The response returns paginated safe historical records and pagination metadata only.

---

## 3. Project Isolation Flow

The request flow is:

1. Dashboard loads project workspace access from Project Service.
2. Project Service validates the authenticated caller against project membership.
3. Project Service resolves active service and device associations.
4. Project Service requests history from Monitoring Service using only associated identifiers.
5. Monitoring Service returns only matching records within the requested range.

Safety rules:

- no global telemetry is presented as project-scoped data
- no project aggregation endpoint is called
- unauthorized access returns `401` or `403` as appropriate
- cross-project telemetry leakage is blocked by backend enforcement

---

## 4. Date-Range and Pagination Rules

### Date range

- `from` and `to` are required
- timestamps use ISO-8601 format
- `from` must not be after `to`
- ranges longer than 90 days are rejected
- malformed timestamps are rejected

### Pagination

- server-side pagination is enforced
- page numbering starts at 0
- page size is limited to 1–100
- sort direction supports `ASC` and `DESC`
- equal timestamps are ordered deterministically

---

## 5. Response Contract

Historical metric responses include safe DTO fields only:

- source type
- source identifier
- metric type
- numeric value
- unit
- status where available
- recorded timestamp
- pagination metadata
- selected date range

No persistence entities are exposed.

---

## 6. Behaviour States

### Project Service states

- `NO_DATA` when the project has no active associations or no safe history is available
- `PARTIAL` when some downstream lookups fail
- `UNAVAILABLE` when downstream retrieval cannot complete safely

### Dashboard states

- loading
- background loading
- empty result
- API error
- unauthorised
- archived project
- partial data
- unavailable data

### Timeline/list UI

The frontend uses a lightweight chronological list rather than advanced charts.

The UI shows:

- source type
- source identifier
- metric type
- value
- unit
- status
- recorded timestamp

Fallback text is displayed when a field is unavailable.

---

## 7. Known Exclusions

SCRUM-694 intentionally excludes:

- metric aggregation
- exports
- advanced filters
- charts beyond the basic timeline/list
- alerts
- incidents
- reports
- forecasting
- AI

Project aggregation remains unsupported and is not used as a fallback.

---

## 8. Validation Evidence

Validated behaviour includes:

- authenticated project historical access
- project-level authorisation
- cross-project `403`
- missing authentication `401`
- associated service/device identifiers only
- no global telemetry fallback
- date range filtering
- 90-day range protection
- ASC and DESC sorting
- deterministic equal-timestamp ordering
- server-side pagination
- empty project handling
- empty selected period handling
- archived project readability
- `PARTIAL` and `UNAVAILABLE` downstream states
- safe handling of downstream failure
- workspace-gated frontend history loading
- pagination boundary behaviour
- page reset on range/size/sort changes
- Version 1.0 dashboard routes remain operational

### Build and test results

- Monitoring Service: `mvn clean test`, `mvn clean package`
- Project Service: `mvn clean test`, `mvn clean package`
- Dashboard: `npm test`, `npm run build`

---

## 9. Dependency Note

SCRUM-694 depends on SCRUM-692 and SCRUM-693.

The workspace foundation and health summary provided by the Project Service are the safe entry points for historical exploration.
