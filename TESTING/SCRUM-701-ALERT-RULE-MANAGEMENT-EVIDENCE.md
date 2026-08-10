# SCRUM-701 Alert Rule Management Evidence

## 1. Business Purpose

SCRUM-701 adds project-scoped configuration management for alert rules. Authorised users can create, view, edit, enable, disable, and delete threshold rules without introducing alert evaluation or notification delivery.

## 2. Architecture Flow

1. The dashboard loads project workspace access from Project Service.
2. After access succeeds, it requests project alert rules through the API Gateway.
3. The Gateway routes `/api/v2/projects/*/alert-rules/**` to Alert Service before the broad project route.
4. Alert Service validates the shared JWT, project role, project status, and optional project associations.
5. AlertRule data is persisted by Alert Service and returned through DTOs.

## 3. AlertRule Model

Fields:

- UUID `id`
- UUID `projectId`
- `name`
- nullable `description`
- `metricType`
- decimal `thresholdValue`
- `comparisonOperator`
- `severity`
- `enabled`
- nullable `deviceId`
- nullable `serviceId`
- `createdAt`
- `updatedAt`

Device and service references are logical identifiers. No cross-service JPA relationships are used. A rule may be project-wide, device-targeted, or service-targeted; device and service targets are mutually exclusive.

## 4. Enums

Metric types:

- `CPU_USAGE`
- `MEMORY_USAGE`
- `TEMPERATURE`
- `RESPONSE_TIME_MS`
- `STATUS_CODE`

Comparison operators:

- `GREATER_THAN`
- `LESS_THAN`
- `GREATER_THAN_OR_EQUAL`
- `LESS_THAN_OR_EQUAL`
- `EQUAL`

Severity values reuse the existing Alert Service enum: `LOW`, `MEDIUM`, `HIGH`.

## 5. Database Migration

Alert Service adds Flyway migration `V2__create_alert_rules_table.sql` for the `alert_rules` table. It includes project, rule configuration, target, enabled-state, and timestamp columns, plus indexes for project, enabled status, and update ordering. A database check constraint prevents simultaneous device and service targets.

The existing `alerts` table is not recreated or modified.

## 6. REST Endpoint Contract

- `GET /api/v2/projects/{projectId}/alert-rules`
- `POST /api/v2/projects/{projectId}/alert-rules`
- `GET /api/v2/projects/{projectId}/alert-rules/{ruleId}`
- `PUT /api/v2/projects/{projectId}/alert-rules/{ruleId}`
- `PATCH /api/v2/projects/{projectId}/alert-rules/{ruleId}/enabled`
- `DELETE /api/v2/projects/{projectId}/alert-rules/{ruleId}`

These endpoints are implemented by the project-scoped AlertRule controller. Responses use DTOs; persistence entities are not exposed.

## 7. Security and Authorization

Alert Service validates the shared EdgeCloud JWT format and requires authentication for `/api/v2/**`. Legacy `/alerts` behavior remains preserved. Actuator health/info endpoints remain available.

Read access is allowed for:

- `ADMIN`
- `PROJECT_ADMIN`
- `OPERATOR`
- `VIEWER`

Mutation access is allowed for:

- `ADMIN`
- `PROJECT_ADMIN`
- `OPERATOR`

`VIEWER` is read-only. Archived projects and cross-project access are denied.

## 8. Association Validation

Alert Service calls the project-scoped Project Service workspace contract with the caller's bearer token. Optional device and service targets must appear in active project association data. No global device or service list is fetched or filtered locally. Authorization and association validation occur before persistence mutation.

## 9. Validation Behaviour

The backend and dashboard validate required fields, trimmed and bounded names, bounded descriptions, finite numeric thresholds, controlled enum values, and device/service mutual exclusion. Project ownership is taken from the URL and not from a request body field.

## 10. Dashboard Route and UI

The dashboard route is `/projects/:projectId/alert-rules`. It provides:

- project context navigation
- workspace-first access loading
- rule count and deterministic rule list
- responsive desktop table and mobile cards
- create/edit dialog
- project-wide, device, and service targeting
- role-aware mutation controls
- enable/disable actions
- delete confirmation
- loading, empty, error, unauthorized, and archived-project states
- mutation success and failure feedback

Project association selectors use only workspace-provided IDs.

## 11. Test Evidence

Automated validation completed:

- Alert Service: 28 tests passed, including Step 2, legacy alert, JWT/controller security, project authorization, association validation, and client propagation tests. `clean compile`, `clean test`, and `clean package` passed.
- API Gateway: 2 tests passed; `clean compile` and `clean package` passed.
- Dashboard: 125 tests passed across 20 files; production build passed.
- Focused dashboard alert-rule suite: 11 tests passed.
- `git diff --check` passed for the code repositories.

## 12. Acceptance Criteria

- AC1 Create Rule: **MET**
- AC2 Edit Rule: **MET**
- AC3 Enable/Disable Rule: **MET**
- AC4 Rule Validation: **MET**
- AC5 Project Isolation: **MET**
- AC6 Rule Listing: **MET**
- AC7 Delete Rule: **MET**

## 13. Manual Evidence

Manual screenshot evidence: **PENDING MANUAL CAPTURE**.

Suggested captures:

- rule list
- create dialog
- edit dialog
- enabled and disabled rules
- device-target rule
- service-target rule
- validation failure
- VIEWER read-only screen
- delete confirmation
- responsive mobile layout

## 14. Out-of-Scope Boundaries

SCRUM-701 does not add:

- rule evaluation
- telemetry evaluation loops
- alert generation from rules
- notifications
- incidents
- acknowledgement
- escalation
- AI threshold generation

## 15. Known Limitations

- Alert rules are configuration only; no rule is evaluated yet.
- Project, device, and service names are not denormalized into Alert Service and may display as IDs.
- Manual browser screenshots remain pending.
- The API Gateway checkout remains on `feature/SCRUM-XXX-project-service-routing`; unrelated JWT-filter, project-route, and test changes require separate branch handling and are excluded from SCRUM-701 staging.
- The documentation directory is not a standalone Git repository in this workspace, so its files require review through the parent documentation repository workflow.
