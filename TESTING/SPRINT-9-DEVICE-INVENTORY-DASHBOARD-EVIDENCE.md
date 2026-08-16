# Sprint 9 Device Inventory Dashboard Evidence

## Automated validation

- Device Service: 28 tests passed, 0 failures, 0 errors, 0 skipped; Java 21 package passed.
- Dashboard: 170 tests passed across 32 files; production build passed.
- Coverage includes retrieval, empty inventory, server-side search, exact ID search, pagination, all supported sorts, invalid parameters, offline visibility, heartbeat derivation, 401, 403, ADMIN access, UI loading/empty/error states, search, sorting, paging and role-aware navigation.

## Runtime validation

Validated through `http://localhost:8095/api/v1/devices/inventory`:

- authenticated ADMIN request: 200;
- unauthenticated request: 401;
- authenticated VIEWER request: 403;
- invalid parameters: 400;
- name and exact-ID searches: one matching device;
- status descending and last-seen ascending sorts echoed correctly;
- the persisted offline device remained visible with `OFFLINE`, `NEVER_RECEIVED`, registration time and null last communication.

Only one persisted device existed, so a multi-page runtime display was not fabricated. Backend paging and Dashboard next-page interaction are covered automatically.

The isolated Device container was rebuilt without deleting volumes. All 15 containers remained running and healthy, and all seven Eureka applications remained `UP`.

## Manual screenshots still required

1. Desktop inventory table with the offline device visible.
2. Tablet-width inventory cards.
3. Search result by name and by device ID.
4. Sort controls and, when sufficient legitimate devices exist, multiple pagination pages.
5. Loading, empty and error presentation where practical.
6. Browser/network evidence for 200, 401, 403 and 400 responses.
7. Docker health and Eureka registrations.

## Known limitations

- Firmware version, tags and location are not stored by Device Service.
- Project assignment is maintained by Project Service and is not exposed by this global inventory query.
- Runtime pagination could not be demonstrated with the single existing device; no artificial persistent devices were created solely for evidence.
