# SCRUM-719 Test and Runtime Evidence

## Automated evidence

- Device Service: 89 tests passed, 0 failures/errors/skips; Java 21 Maven clean test and package passed.
- Dashboard: 190 tests passed across 36 files; production build and scoped ESLint passed.
- Controlled policy performance: 10,000 sequential calculations completed in 7 ms on the final run (assertion `< 1,000 ms`). This excludes HTTP, database, Docker, and network latency and is not a production SLA.
- Flyway migration, controller security, project isolation, history pagination/order, state boundaries, recovery, configuration, inventory composition, and UI states are covered.

## Runtime evidence

The Java 21 artefact was deployed to the existing Device Service container without rebuilding images or deleting volumes. Through Gateway, the registered device progressed `ONLINE` (0 missed) → `HEALTHY` (1) → `DELAYED` (2) → `OFFLINE` (3), then a new heartbeat returned it to `ONLINE` and populated `lastRecoveryAt`. `lastHeartbeat` and `nextExpectedHeartbeat` were returned, five ordered history events were persisted, and the `OFFLINE` inventory filter returned the device.

An invalid 5-second interval/10-second timeout policy returned `400`; the valid 5/15 policy enabled the transition observation and was then restored to 30/90. Unauthenticated inventory returned `401`, a random cross-project heartbeat request returned `403`, and controller tests verify `VIEWER` denial. Existing project/group/tag filter composition is covered by backend and Dashboard regression tests; no runtime projects existed to mutate safely for an additional live combination.

All 15 containers were healthy afterward. Eureka reported all seven applications `UP`. Docker Compose configuration parsed successfully (expected unset-local-environment warnings only). No volume or existing user data was destroyed.

## Manual screenshot checklist

All remain **PENDING MANUAL CAPTURE**:

- online/healthy, delayed, offline, and recovered devices
- heartbeat details and history
- policy configuration and invalid-policy response
- heartbeat inventory filtering and responsive/tablet view
- representative API and `401`/`403` responses
- controlled performance result
- Docker Compose health and Eureka registrations

## Limitations

The existing heartbeat ingestion path relies on Gateway JWT protection; per-device credentials are outside SCRUM-719. State filters use the last scheduled persisted evaluation while individual state reads calculate from the current timestamp. Manual visual screenshots cannot be captured as repository evidence automatically.
