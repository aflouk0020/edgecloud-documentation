# SCRUM-718 Device Organisation Evidence

## Automated evidence

- Device Service: group/tag CRUD, name normalisation and duplicates, multi-device/idempotent membership, deletion safeguards, replacement tag assignment, cross-project rejection, composed group/tag/search/page/sort specifications, offline inventory regression, JWT and role checks.
- Dashboard: organisation loading/empty/error/create flows; project/group/multiple-tag composition and clear controls; navigation roles; existing inventory tests.
- Gateway: specific Alert Service project routes remain ahead of the broad Project Service route.
- Migration: additive V4 only; indexed logical project scope; no cross-service database foreign key.

Final automated results: Device Service **78/78**, Gateway **6/6**, and Dashboard **187/187** tests passed. Device Service and Gateway Maven packages and the Dashboard Vite production build passed. The pre-existing repository-wide ESLint baseline remains non-zero outside this story; SCRUM-718 files introduced no remaining lint findings.

## Gateway runtime evidence

All requests below traversed `localhost:8095` with persistent MySQL volumes retained. Duplicate normalised group creation returned `409`; populated-group deletion returned `409`; group membership returned one device; three tags were assigned; group, two-tag AND, and combined search/group/tag/sort filters each returned the expected single OFFLINE device. Unauthenticated access returned `401`, a non-accessible project returned `403`, tag removal retained the remaining assignments, both empty groups deleted with `204`, and the device still existed afterward. Temporary organisation metadata and the temporary project association were removed.

All 15 containers were running, Device Service and Gateway actuator health returned `UP`, and the seven Eureka applications were registered `UP`. A targeted no-build container replacement was used because host free space was only 661 MiB; no Docker volume or database data was removed.

## Manual screenshot checklist

- Device Inventory with project, group and two tag filters active
- Group management with membership list
- Multi-tag assignment and tag chips
- Populated-group deletion conflict message
- Responsive tablet inventory/dialog
- Docker Compose health and seven Eureka applications UP

Status: **PENDING MANUAL CAPTURE**.
