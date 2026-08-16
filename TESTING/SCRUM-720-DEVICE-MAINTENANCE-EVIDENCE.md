# SCRUM-720 Test, Runtime, and Evidence Record

## Automated validation

- Device Service: **101/101 passed**, zero failures/errors/skips.
- Dashboard: **196/196 passed across 37 files**.
- Targeted Dashboard maintenance tests: **15/15 passed**.
- Java 21 clean package: passed.
- Dashboard production build: passed; existing bundle-size advisory only.
- Scoped ESLint and `git diff --check`: passed.
- Docker Compose configuration: passed with expected unset-local-environment warnings.

Coverage includes enable/disable, idempotency, conflict and payload validation, immutable history, automatic expiry, heartbeat continuity, inactive/deleted behaviour, authentication, RBAC, project isolation, inventory projection, responsive UI semantics, confirmations, and loading/empty/error states.

## Runtime evidence

Validation used API Gateway and controlled existing/temporary device data:

- initial current state returned maintenance disabled;
- enable returned `200`, reason/actor/timestamps/end, and inventory updated immediately;
- exact duplicate returned `200`; incompatible re-enable returned `409`;
- heartbeat ingestion succeeded during maintenance and heartbeat history increased **9 → 10**;
- manual disable and repeated disable returned `204`;
- history recorded `ENABLED` and `DISABLED`;
- scheduled maintenance expired automatically and recorded exactly one `EXPIRED` event;
- the device remained registered and resumed normal heartbeat state;
- inactive enable returned `409`; inactive read/disable returned `200/204`;
- deleted temporary-device current lookup returned `404`, while retained history returned `200`;
- configuration was unchanged; groups/tags/registration/lifecycle were preserved;
- Monitoring Service retained all **7** existing telemetry rows.

Correct-project read/enable/disable returned `200/200/204`; cross-project read/mutation returned `403`. Security observations were unauthenticated `401`, `VIEWER` `403`, `PROJECT_ADMIN` mutation `403`, `ADMIN` permitted, `OPERATOR` `200/204`, invalid payload `400`, and missing device `404`.

Flyway V6 existed exactly once before and after restart. All **15** containers were healthy, all **7** Eureka applications were `UP`, and Device Service/Gateway health returned `200`.

## Manual evidence checklist

Every browser screenshot below is **PENDING MANUAL CAPTURE**:

- [ ] Inventory maintenance badge — **PENDING MANUAL CAPTURE**
- [ ] Responsive maintenance card — **PENDING MANUAL CAPTURE**
- [ ] Enable dialog and confirmation — **PENDING MANUAL CAPTURE**
- [ ] Reason and optional scheduled end — **PENDING MANUAL CAPTURE**
- [ ] Active maintenance details, actor, and timestamps — **PENDING MANUAL CAPTURE**
- [ ] Maintenance history — **PENDING MANUAL CAPTURE**
- [ ] Separate `ENABLED`, `DISABLED`, and `EXPIRED` events — **PENDING MANUAL CAPTURE**
- [ ] Disable confirmation — **PENDING MANUAL CAPTURE**
- [ ] ADMIN/OPERATOR controls and absence of PROJECT_ADMIN/VIEWER mutation controls — **PENDING MANUAL CAPTURE**
- [ ] Validation/error/success/loading feedback — **PENDING MANUAL CAPTURE**
- [ ] Heartbeat continuing during active maintenance — **PENDING MANUAL CAPTURE**
- [ ] Representative `200`, `204`, `400`, `401`, `403`, and `404` API responses — **PENDING MANUAL CAPTURE**
- [ ] All 15 healthy Docker containers — **PENDING MANUAL CAPTURE**
- [ ] Seven Eureka applications `UP` — **PENDING MANUAL CAPTURE**
- [ ] Device/Dashboard test totals, builds, and lint — **PENDING MANUAL CAPTURE**

## Limitations

There is no scheduled future start, remote configuration distribution, remote command/remediation, firmware operation, or duplication of Alert Service maintenance windows. Actor names are not resolved from UUIDs. The automated browser surface was unavailable during runtime validation, so interactive screenshot validation remains pending and is not claimed as completed evidence.
