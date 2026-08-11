# SCRUM-712 Alert Escalation Policy Engine Evidence

| Requirement | Evidence |
|---|---|
| Scheduled evaluation | Configurable scheduler and bounded active-alert query operated in Docker. |
| Unacknowledged | Runtime OPEN alert produced levels 1 and 2 with `UNACKNOWLEDGED` history. |
| Acknowledged unresolved | Controlled ACKNOWLEDGED alert produced `UNRESOLVED` history. |
| Multiple levels | Local 2-second/40-second policy produced ordered levels 1 and 2. |
| Duplicate prevention | A later scheduler cycle retained exactly two levels/source events. |
| Notifications | Two source events produced four authorised notifications and four delivered escalation emails. |
| Security | Unauthenticated request 401, VIEWER mutation 403, unrelated project 404. |
| Persistence | Alert V6 and Notification V5 applied once on MySQL; public history API returned persisted entries. |

Automated validation: Alert Service 115 tests; Notification Service 56 tests; Gateway 6 tests; Dashboard full suite 157 tests. All passed, and service/dashboard packages built successfully.

This is controlled local Docker/MySQL/Mailpit acceptance evidence. Short thresholds are test data, not production defaults or an SLA. Manual screenshots remain **PENDING MANUAL CAPTURE**.
