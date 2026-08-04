# SCRUM-698 — Real-Time Observability Updates Evidence

## 1. Story purpose

SCRUM-698 introduces shared polling for project observability so dashboards refresh automatically without manual reloads while preserving project isolation and existing Version 1.0 routes.

## 2. Polling-based architecture

The dashboard now uses a shared polling foundation instead of page-local timers. The page-level observability views reuse a common polling hook, shared configuration, and a shared connection-status component.

WebSockets and Server-Sent Events remain out of scope because the story is explicitly polling-based and does not require push infrastructure.

## 3. Shared polling hook

The shared hook is responsible for:

- one in-flight request per resource
- bounded retry/backoff
- hidden-tab pause and visibility recovery
- cleanup of timers and listeners on unmount
- connection-state reporting

## 4. Central refresh configuration

Refresh intervals are centrally configured and clamped by the existing rules.

- Summary polling default: 60 seconds
- Historical polling: slower than summary polling
- Historical polling only occurs on page 0

## 5. Connection states

The UI displays:

- Connected
- Refreshing
- Degraded
- Disconnected

The connection state is readable and not colour-only.

## 6. Last successful refresh timestamp

Each migrated page shows the latest successful refresh timestamp so operators can distinguish live refreshes from stale data.

## 7. Refresh warning

Background failures keep prior data visible and show a non-intrusive warning. Successful recovery clears the warning.

## 8. Page coverage

### Project Workspace

- shared summary polling
- latest successful refresh timestamp
- workspace access before polling

### Project Service Health

- shared service-health polling
- sorting preserved across refreshes
- 401/403 stop polling

### Project Device Health

- shared device-health polling
- sorting preserved across refreshes
- 401/403 stop polling

### Project Historical Metrics

- polling only on page 0
- manual refresh on every page
- filters and pagination preserved

## 9. Failure handling

- first-load failure uses the page’s existing fatal error state
- background failure retains existing data
- 401/403 stop automatic polling
- retry/backoff is bounded

## 10. Project isolation

Polling requests are only issued after workspace access succeeds. The frontend never falls back to global telemetry or global service/device collections for project-scoped observability.

## 11. Request-frequency rationale

Polling frequency is intentionally modest:

- summary-style views: 60 seconds
- historical metrics: slower than summary polling and only on the first page

This balances freshness with predictable API load.

## 12. Known limitations

- No WebSockets or SSE
- No user-editable polling settings
- No backend combined-refresh endpoint
- No alerts, incidents, or push-based updates

## 13. Final validation results

Dashboard verification completed successfully:

- `npx vitest run src/config/observabilityRefreshConfig.test.js`
- `npx vitest run src/hooks/useObservabilityPolling.test.jsx`
- `npx vitest run src/components/observability/ObservabilityConnectionStatus.test.jsx`
- `npx vitest run src/pages/projects/ProjectWorkspacePage.test.jsx`
- `npx vitest run src/pages/projects/ProjectServiceHealthPage.test.jsx`
- `npx vitest run src/pages/projects/ProjectDeviceHealthPage.test.jsx`
- `npx vitest run src/pages/projects/ProjectHistoricalMetricsPage.test.jsx`
- `npm test`
- `npm run build`

Observed result:

- 91 dashboard tests passed
- production build passed

## 14. Evidence checklist

Captured in code and test output:

- automatic project-health refresh
- automatic service-health refresh
- automatic device-health refresh
- historical page-0 polling
- no polling on historical page 1+
- Connected / Refreshing / Degraded / Disconnected states
- last successful refresh display
- background failure with data retained
- successful recovery
- hidden-tab pause
- visibility recovery
- 401 handling
- 403 handling
- frontend test output
- production build output

Pending manual screenshot evidence:

- desktop layout
- tablet layout
- mobile layout

