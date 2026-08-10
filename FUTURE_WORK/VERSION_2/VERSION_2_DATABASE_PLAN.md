# EdgeCloud Platform Version 2.0 Database Plan

## 1. Purpose

This document defines the database planning approach for EdgeCloud Platform Version 2.0.

It establishes:

- Data ownership
- Service boundaries
- Migration principles
- Retention requirements
- Indexing expectations
- Audit requirements
- Reporting considerations
- Version 1.0 compatibility rules

The objective is to support reliable growth without creating shared-database coupling.

---

## 2. Core Database Principles

Version 2.0 must follow these principles:

- Every microservice owns its database.
- Services must not access another service's database directly.
- Cross-service references must use logical identifiers.
- Database changes must use controlled migrations.
- Existing Version 1.0 data must remain valid.
- High-volume data must have retention rules.
- Frequently queried fields must be indexed.
- Sensitive data must be protected.
- Reporting must not compromise transactional services.

---

## 3. Current Version 1.0 Data Domains

The existing platform includes data associated with:

| Domain | Primary Owner |
| --- | --- |
| Users and authentication | Authentication Service |
| Devices | Device Service |
| Telemetry and metrics | Monitoring Service |
| Alerts | Alert Service |
| Service discovery metadata | Discovery Service runtime |

Version 2.0 must extend these domains without removing existing behaviour.

---

## 4. Proposed Version 2.0 Data Domains

| Domain | Proposed Owner |
| --- | --- |
| Projects | Project Service |
| Project membership | Project Service |
| Project service associations | Project Service |
| Project device associations | Project Service |
| Repository metadata | Integration Service |
| Webhook events | Integration Service |
| Build executions | DevOps capability |
| Build stages | DevOps capability |
| Test results | Quality Service or DevOps capability |
| Quality findings | Quality Service |
| Deployments | DevOps capability |
| Incidents | Alert Service or Incident capability |
| Analytics summaries | Analytics Service |
| Organisations | Organisation capability |
| Organisation membership | Organisation capability |
| Audit events | Audit capability or owning service |

Final ownership must be confirmed through architecture decisions before implementation.

---

## 5. Project Service Data Plan

The Project Service is expected to own:

- Projects
- Project members
- Project roles
- Project-to-service associations
- Project-to-device associations
- Project metadata
- Project status
- Project timestamps

Suggested project fields include:

| Field | Purpose |
| --- | --- |
| id | Unique project identifier |
| name | Human-readable project name |
| description | Project purpose |
| status | Active, archived or suspended state |
| owner_user_id | Logical reference to the owner |
| organisation_id | Optional logical organisation reference |
| created_at | Creation timestamp |
| updated_at | Last update timestamp |

Project identifiers should be immutable.

---

## 6. Monitoring Data Plan

Monitoring data is expected to remain owned by the Monitoring Service.

Important considerations include:

- Metric timestamp
- Device identifier
- Service identifier
- Project identifier
- Metric type
- Metric value
- Unit
- Source
- Agent version

High-volume monitoring data must support:

- Time-range queries
- Pagination
- Aggregation
- Retention
- Downsampling
- Efficient deletion

Project identifiers may be stored as logical references for query efficiency.

---

## 7. Device Data Plan

The Device Service should continue owning device information.

Version 2.0 may extend device records with:

- Project identifier
- Agent version
- Last heartbeat
- Operating system
- Architecture
- Environment
- Connection state
- Registration status

Device ownership must remain separate from monitoring-history ownership.

---

## 8. Alert and Incident Data Plan

### Implemented baseline through SCRUM-703

Alert Service now owns an `alert_events` history table containing alert/rule/project identity, rule-name snapshot, source identity, metric evidence, threshold/operator/severity snapshots, OPEN/RESOLVED status, and trigger/observation/resolution/audit timestamps. A generated `open_marker` is `1` for OPEN and `NULL` for RESOLVED. A composite unique key over project, rule, source type, source ID, metric type, and this marker permits historical RESOLVED rows while preventing more than one active OPEN row.

Acknowledgement, assignment, notification, escalation, suppression, and incident data remain unimplemented future extensions.

Alert data may include:

- Alert identifier
- Project identifier
- Source identifier
- Alert rule
- Severity
- State
- Triggered timestamp
- Acknowledged timestamp
- Resolved timestamp
- Assigned user
- Deduplication key

Incident functionality may extend alerts with:

- Incident title
- Incident description
- Timeline events
- Assigned owner
- Resolution summary
- Related alerts
- Related deployments

The final incident ownership model must be decided before implementation.

---

## 9. Integration Data Plan

The Integration Service may own:

- Repository connections
- Provider name
- Repository owner
- Repository name
- Default branch
- Installation identifiers
- Webhook configuration
- Last synchronisation state
- Integration health
- Received webhook-event metadata

Provider secrets and access tokens must not be stored in plain text.

Webhook payload retention should be limited to operational need.

---

## 10. Build and Quality Data Plan

Build data may include:

- Build identifier
- Project identifier
- Repository identifier
- Commit SHA
- Branch
- Trigger type
- Status
- Started timestamp
- Completed timestamp
- Duration
- Runner identifier

Build-stage data may include:

- Stage name
- Execution order
- Status
- Started timestamp
- Completed timestamp
- Log reference

Quality data may include:

- Test count
- Passed tests
- Failed tests
- Skipped tests
- Coverage percentage
- Quality finding category
- Severity
- File path
- Line number
- Status

Large logs should be stored separately from core relational records where appropriate.

---

## 11. Analytics Data Plan

The Analytics Service should use read-oriented data models.

Possible analytics records include:

- Daily project health
- Build success rate
- Deployment frequency
- Mean build duration
- Alert count
- Incident count
- Device availability
- Service availability
- Quality trend
- Test trend

Analytics models should be regenerated or repaired without changing transactional source data.

---

## 12. Organisation Data Plan

Enterprise functionality may require:

- Organisations
- Organisation members
- Organisation roles
- Project ownership
- Subscription or plan metadata
- Organisation status

Organisation scope must not be introduced until access-control rules are clearly defined.

Cross-tenant isolation must be tested at repository, service and controller levels.

---

## 13. Audit Data Plan

Audit events should capture significant actions such as:

- Authentication changes
- Project creation
- Membership changes
- Role changes
- Repository connections
- Build execution
- Deployment actions
- Alert acknowledgement
- Incident resolution
- Organisation administration

Suggested audit fields include:

| Field | Purpose |
| --- | --- |
| id | Unique audit identifier |
| actor_user_id | User who performed the action |
| action | Recorded action |
| resource_type | Type of affected resource |
| resource_id | Logical resource identifier |
| project_id | Related project |
| organisation_id | Related organisation |
| timestamp | Time of the action |
| outcome | Success or failure |
| metadata | Limited contextual information |

Audit records should be append-only.

---

## 14. Migration Standards

All schema changes must use migration scripts.

Migration rules:

- Never rely on manual production changes.
- Use ordered migration versions.
- Keep migrations small.
- Test migrations on representative data.
- Preserve existing records.
- Document destructive changes.
- Define rollback or recovery steps.
- Back up important data before high-risk migrations.

A migration must be reviewed before release.

---

## 15. Indexing Standards

Indexes should be considered for:

- Foreign logical identifiers
- Project identifiers
- Organisation identifiers
- Device identifiers
- Service identifiers
- Status fields
- Timestamp fields
- Commit SHA
- Repository identifiers
- Alert severity
- Incident state

Indexes should be based on real query patterns rather than added without evidence.

---

## 16. Retention Standards

Retention policies are required for:

- Raw telemetry
- Build logs
- Webhook payloads
- Audit records
- Alert history
- Incident history
- Generated reports
- Temporary runner data

Retention periods must balance:

- Operational value
- Storage cost
- Security
- Academic evidence
- Compliance needs

Temporary build workspaces must be deleted after execution.

---

## 17. Data Validation

Database and service-level validation should protect:

- Required fields
- Field lengths
- Supported statuses
- Numeric ranges
- Timestamp consistency
- Duplicate records
- Ownership scope
- Immutable identifiers

Validation must not rely only on frontend controls.

---

## 18. Transaction Standards

Transactions should remain within a service boundary.

Distributed transactions should be avoided.

Cross-service workflows should use:

- Idempotent APIs
- Retry-safe operations
- Explicit failure states
- Eventual consistency where appropriate
- Compensating actions where required

---

## 19. Backup and Recovery

Important databases should have:

- Backup procedures
- Restore procedures
- Recovery verification
- Migration rollback guidance
- Clear ownership
- Documented storage locations

A backup is not considered reliable until restoration has been tested.

---

## 20. Reporting Considerations

Reports should be generated from:

- Approved service APIs
- Analytics read models
- Controlled exports

Reports must not use direct cross-service database queries.

Generated reports should record:

- Generation timestamp
- Project scope
- Reporting period
- Data source
- Report version

---

## 21. Database Review Checklist

Before implementing a database change, confirm:

- The owning service is clear.
- The change does not create cross-service coupling.
- Migration scripts are planned.
- Existing data remains valid.
- Required indexes are identified.
- Retention impact is understood.
- Security impact is reviewed.
- Backup needs are considered.
- Tests are defined.
- Documentation will be updated.

---

## 22. Current Status

**Status:** Draft

**Owner:** Taha Aflouk

**Version:** EdgeCloud Platform Version 2.0

**Previous document:** VERSION_2_DEPENDENCY_MATRIX.md

**Next document:** VERSION_2_API_PLAN.md
