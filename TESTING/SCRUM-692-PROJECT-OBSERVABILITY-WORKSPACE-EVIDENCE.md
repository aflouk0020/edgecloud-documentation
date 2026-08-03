# SCRUM-692 Project Observability Workspace Evidence

## 1. Scope

SCRUM-692 delivered the first safe Project Observability Workspace for EdgeCloud Monitor Version 2.0.

The implementation stays inside the Project Service boundary for workspace ownership and uses the existing Dashboard only as a presentation layer. It does not introduce project aggregation and does not represent global telemetry as project-scoped data.

---

## 2. Workspace contract

The Project Service now exposes a workspace summary at:

```http
GET /api/v2/projects/{projectId}/workspace
```

The response includes only safe workspace data:

- project identity
- project status
- caller project role
- associated service identifiers
- associated device identifiers
- association counts
- empty-workspace indicators
- generated timestamp

The contract intentionally returns identifiers only for associated services and devices. Enrichment happens later in the dashboard and only after workspace access succeeds.

---

## 3. Project authorisation model

Workspace access is enforced in the Project Service using the existing EdgeCloud JWT contract and project membership rules.

Authorisation summary:

- `ADMIN` can access any project workspace
- `PROJECT_ADMIN`, `OPERATOR`, and `VIEWER` can access their active assigned workspace
- inactive members are denied
- cross-project access is denied
- archived projects remain viewable but clearly report archived status

---

## 4. Frontend route and layout

The dashboard exposes a project-centred route:

```http
/projects/:projectId/workspace
```

The page uses the existing authenticated dashboard shell and keeps Version 1.0 routes intact.

Workspace layout includes:

- project summary header
- local project navigation placeholders
- service section
- device section
- loading state
- empty state
- error state
- unauthorised state
- archived-project state
- partial-success state for enrichment

---

## 5. Service and device enrichment flow

The dashboard loads the workspace summary first.

Only after that succeeds does it request safe details for the service IDs and device IDs returned by the workspace response.

Safety rules:

- no enrichment before workspace access succeeds
- only workspace-returned identifiers are requested
- unavailable items fall back to identifier-only display
- one failed lookup does not break the page
- no global telemetry is displayed as project-scoped data

---

## 6. Validation evidence

Validated behaviour includes:

- authenticated project workspace access
- project context displayed correctly
- missing authentication returns `401`
- unauthorised project access returns `403`
- empty workspace renders safely
- archived workspace renders safely
- associated services are displayed
- associated devices are displayed
- partial enrichment failures do not break the page
- only workspace-returned identifiers are requested
- existing Version 1.0 dashboard routes continue to work

---

## 7. Known limitation

Project-level metric aggregation remains unsupported in Monitoring Service and is intentionally not used by this workspace.

This is a deliberate safety boundary until project-scoped observability aggregation is wired to the Project Service source of truth.

---

## 8. Testing and build evidence

Final validation for the SCRUM-692 workspace included:

- backend compile and test validation for Project Service
- frontend test and build validation for Dashboard
- route and authorisation checks
- workspace loading and enrichment checks

