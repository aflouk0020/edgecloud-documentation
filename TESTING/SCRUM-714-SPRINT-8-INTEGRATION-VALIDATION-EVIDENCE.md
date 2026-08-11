# SCRUM-714 Sprint 8 Integration Validation Evidence

## Scope and commands

This is a controlled local integration/regression run on Java 21 and the existing Docker/MySQL/Mailpit environment. It is not production certification.

```text
./mvnw test                         # Monitoring, Alert, Gateway, Device, Auth
mvn test                            # Notification, Project
npm test -- --run && npm run build  # Dashboard
docker compose --env-file ../env/.env -f docker-compose.yml config -q
docker compose --env-file ../env/.env -f docker-compose.yml up -d --no-deps --no-build --force-recreate monitoring-service
docker ps; docker stats --no-stream; GET /eureka/apps
curl through Gateway for telemetry and representative Sprint 8 V2 APIs
```

## Automated regression

| Component | Result |
|---|---:|
| Monitoring Service | 68/68 passed |
| Alert Service | 124/124 passed, including MySQL concurrency |
| Notification Service | 56/56 passed |
| API Gateway | 6/6 passed |
| Dashboard | 160/160 passed; production build passed |
| Project Service | 218/218 passed; unpublished SCRUM-711 recipient resolution reconciled in PR #9 |
| Auth Service | 10/10 passed; unpublished SCRUM-711 identity resolution reconciled in PR #9 |
| Device Service | 19/19 passed after replacing a wall-clock-expired fixed test JWT with a bounded current test token |

The first highly parallel Dashboard run exposed three timing-sensitive filter-chip test failures; an immediate complete retry passed all 160 tests. No product code was changed for the retry.

## Runtime integration

- Compose configuration validated. All 15 EdgeCloud containers were healthy and all seven Eureka applications reported `UP`.
- Ordinary Monitoring Service recreation retained its telemetry row count (`1 -> 1`), confirming database data survived restart.
- The Compose hardening supplied Monitoring with its Project and Alert service-network URLs. Five Gateway telemetry submissions then persisted five rows and produced five suppression records during an active project window, with zero AlertEvents and zero outbox entries.
- After authoritative expiry, another Gateway telemetry submission returned 201 and produced one AlertEvent and one OPENED outbox. The outbox reached `PUBLISHED`, creating two recipient notifications and four `DELIVERED` in-app/email channel records.
- The alert progressed through escalation levels 1 and 2 exactly once each (`2 rows / 2 distinct levels`). Acknowledgement persisted one ownership-history record; repeat acknowledgement was idempotent and a different VIEWER could not release ownership.
- Replaying one identical evaluation changed `duplicate` from `false` to `true` and retained exactly one suppression row.
- Alert Flyway latest version was 7 with six successful versioned migrations (V2–V7). Notification latest was V5 with five successful migrations. Project V1 was present once. The other current services use their existing Hibernate-managed schemas.

## API and security observations

Representative Gateway GETs for alert rules, alerts, escalation policy, maintenance windows and user notifications returned 200. Unauthenticated public and direct internal Alert requests returned 401; VIEWER maintenance mutation and cross-user ownership release returned 403; malformed maintenance time range returned 400; inaccessible random project returned the established secure 404 response.

## Controlled processing observation

Five sequential end-to-end Gateway telemetry calls during maintenance completed correctly: minimum 109.0 ms, maximum 1,057.0 ms, average 368.3 ms. Every sample persisted and was evaluated, no duplicate alert/outbox appeared, containers remained healthy, and no obvious resource failure occurred. Snapshot resource use was approximately Monitoring 443 MiB, Alert 555 MiB, Notification 532 MiB and Gateway 341 MiB, with low single-digit CPU. These local observations are not a production SLA or load certification.

## Known limitations

- The Dashboard timing-sensitive filter-chip tests passed on the clean full retry but should be monitored for future CI flakiness.

The pre-existing Project and Auth SCRUM-711 working trees were contract-checked against Notification Service, rebuilt on Java 21, and merged through their respective PR #9. Both repositories were returned to clean, updated `main`.

## Manual evidence checklist

Manual screenshots remain **PENDING MANUAL CAPTURE**:

1. Project Alert History showing the alert owner, acknowledgement history and both escalation levels.
2. Maintenance page showing the expired SCRUM-714 window and suppression history containing all five suppressed evaluations.
3. Notification panel showing delivered OPENED and escalation notifications for the resolved recipients.
4. Docker Desktop or `docker compose ps` showing all 15 containers healthy.
5. Eureka Applications page showing all seven EdgeCloud applications registered `UP`.
