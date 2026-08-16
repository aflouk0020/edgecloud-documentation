# Sprint 9 Device Registration and Lifecycle Evidence

## Automated validation

- Device Service: 40 tests passed; clean Maven package completed on Java 21.
- Dashboard: 174 tests across 33 files passed; Vite production build completed.
- Focused lifecycle tests cover registration, duplicate prevention, metadata update, deactivate/reactivate, guarded deletion, retained history, missing devices, JWT authentication, and ADMIN/OPERATOR/VIEWER authorization.
- UI tests cover mandatory-field validation, registration, editing, history rendering, inventory regression, search, sort, pagination, loading, empty, error, and offline display.

## Runtime evidence

Focused validation against the persistent local MySQL environment passed through API Gateway: registration `201`, duplicate rejection `409`, metadata update `200`, inventory search `200` with one match, deactivate `200`, inactive heartbeat rejection `409`, reactivate `200`, second deactivate `200`, history `200`, guarded deletion `204`, and post-delete history `200` with all six events retained. Unauthenticated access returned `401` and a valid VIEWER token returned `403`.

All 15 running containers reported healthy, all seven Eureka applications reported UP, and Device Service health returned `200`. Existing Docker volumes were preserved. Because Docker Hub metadata access stalled, the already-built tested application JAR was copied into and restarted within the existing Device Service container for focused runtime validation; no image was published and no Docker data was removed.

## Manual screenshot checklist

- ADMIN `/devices` inventory with active and inactive devices.
- Register form and successful refreshed inventory row.
- Edited metadata, including location/firmware/operating system.
- Duplicate or validation feedback.
- Deactivate and Reactivate actions/status.
- Lifecycle history dialog.
- Explicit removal confirmation.
- Docker Compose health and Eureka Device Service UP.

## Known limitation

Project assignment is managed by Project Service and is not mutated by this story. External telemetry history is intentionally not deleted. Manual screenshots remain pending capture.
