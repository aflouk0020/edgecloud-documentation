# SCRUM-717 Device Configuration Management Evidence

## Automated validation

- Device Service: 58 tests passed; Java 21 clean Maven package passed.
- Dashboard: 182 tests across 34 files passed; Vite production build passed.
- Focused backend coverage includes defaults, update/version creation, idempotent unchanged PUT, history order, restore/new version, template uniqueness/application, failure propagation for transactional rollback, inactive/missing devices, metadata preservation, validation, JWT, role authorization, and platform/project-role isolation.
- Focused UI coverage includes loading/rendering, validation, save, API failure, templates, confirmed restore, inactive state, roles, and existing inventory regressions.

## Runtime evidence

Focused persistent-MySQL validation passed through Gateway: default read `200` at version 0; invalid update `400`; two valid updates `200`; ordered history `200`; restore version 1 `200` as version 3; template creation `201`; template application `200` as version 4; and four immutable history snapshots. The final template values and `STORED_ONLY` state were returned correctly. Device metadata was byte-for-byte unchanged before and after configuration operations.

Unauthenticated access returned `401`; VIEWER and PROJECT_ADMIN returned `403`. After deactivation, configuration remained readable `200` while update returned `409`; guarded device cleanup returned `204`. All 15 containers were healthy and all seven Eureka applications were UP. Existing volumes were preserved.

Host free space was only about 599 MiB, so a Docker image build was unsafe. The tested packaged JAR was copied into and restarted inside the existing Device Service container to apply Flyway V3 and perform focused validation. No images, volumes, or Docker data were deleted.

## Manual screenshot checklist

- Configuration dialog and centrally-stored-only notice.
- Validation and backend error feedback.
- Successful save and incremented version.
- Template selection/application and ADMIN template editor.
- Version history with actor, timestamp, action, and changed fields.
- Restore confirmation and resulting new version.
- Inactive read-only view.
- Docker health and Eureka registrations.

Manual screenshots remain pending capture. Remote configuration distribution/synchronisation is out of scope.
