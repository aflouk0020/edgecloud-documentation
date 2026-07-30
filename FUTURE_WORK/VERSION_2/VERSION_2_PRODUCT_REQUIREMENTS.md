# EdgeCloud Platform Version 2.0 Product Requirements

## 1. Document Purpose

This document defines the functional, non-functional, security, operational and quality requirements for EdgeCloud Platform Version 2.0.

It converts the approved product vision into measurable platform requirements that will guide architecture design, Jira backlog creation, implementation, testing and release acceptance.

This document does not define individual Jira stories. Detailed stories will be derived later through the Version 2.0 Jira roadmap.

---

## 2. Product Context

EdgeCloud Monitor Version 1.0 provides a working cloud-native monitoring platform with:

- Spring Boot microservices
- Netflix Eureka service discovery
- API Gateway routing
- JWT authentication
- Role-based access control
- Monitoring Service
- Device Service
- Alert Service
- React dashboard
- Raspberry Pi telemetry agent
- Heartbeat processing
- Historical telemetry
- Threshold-based alerting
- Docker Compose deployment

Version 2.0 must preserve these capabilities while extending the product into a unified Engineering Operations Platform.

The expanded platform will support:

- Software projects
- Repositories
- Microservices
- Edge devices
- Builds
- Tests
- Code quality
- Quality gates
- Deployments
- Runtime monitoring
- Alerts
- Incidents
- Analytics
- Reporting
- Organisations
- Teams
- Role-based governance

---

## 3. Product Objectives

The Version 2.0 product requirements must support the following objectives:

1. Preserve the working Version 1.0 monitoring platform.
2. Introduce project-oriented organisation.
3. Support monitoring of microservices and edge devices.
4. Provide engineering workflow visibility.
5. Reduce dependence on separate Jenkins and SonarQube installations.
6. Support developers, managers, students and business stakeholders.
7. Provide professional dashboards and reports.
8. Introduce secure organisation and tenant foundations.
9. Maintain Docker-based deployment.
10. Create a reliable foundation for future SaaS operation.

---

## 4. Product Actors

### 4.1 Platform Administrator

The Platform Administrator manages:

- Platform configuration
- Organisations
- Users
- Roles
- Projects
- System-wide policies
- Audit records
- Platform health
- Retention settings
- Integration settings

### 4.2 Organisation Administrator

The Organisation Administrator manages:

- Organisation users
- Organisation teams
- Organisation projects
- Organisation integrations
- Access permissions
- Organisation reports

### 4.3 Project Administrator

The Project Administrator manages:

- Project settings
- Repositories
- Services
- Devices
- Builds
- Deployments
- Quality gates
- Alert rules
- Project members

### 4.4 Developer

The Developer can:

- View assigned projects
- View repositories
- Trigger permitted builds
- Review build results
- Review tests
- Review code-quality findings
- View deployments
- View service metrics
- View alerts and incidents
- Acknowledge permitted alerts

### 4.5 DevOps or Platform Engineer

The DevOps or Platform Engineer can:

- Configure monitoring
- Configure build and deployment workflows
- Review container and service health
- Manage alert rules
- Investigate incidents
- Review operational metrics
- Manage runtime integrations

### 4.6 Technical Manager

The Technical Manager can:

- View project health
- View quality-gate status
- View deployment trends
- View reliability indicators
- View incident summaries
- Generate reports
- Review engineering performance

### 4.7 Business Viewer

The Business Viewer can access approved high-level information including:

- Project status
- Availability
- Delivery confidence
- Risk summaries
- Incident impact
- Business-focused reports

### 4.8 Student

The Student can:

- Register or access learning projects
- View build and test results
- Review code quality
- View monitoring results
- Generate evidence reports
- Understand pipeline stages and failures

### 4.9 Read-Only Auditor

The Read-Only Auditor can:

- View approved project records
- View deployment history
- View audit records
- View quality-gate decisions
- View incident history
- Export compliance evidence

---

## 5. Functional Requirements

# 5.1 Project Management Requirements

### FR-PROJ-001 — Project Registration

The platform shall allow authorised users to create a software project.

A project shall include:

- Unique identifier
- Project name
- Description
- Owning organisation
- Project status
- Visibility
- Created date
- Updated date
- Created-by user
- Default branch
- Optional tags

### FR-PROJ-002 — Project Update

The platform shall allow authorised users to update project metadata.

### FR-PROJ-003 — Project Archiving

The platform shall support archiving projects without immediately deleting historical records.

### FR-PROJ-004 — Project Membership

The platform shall support assigning users and teams to projects.

### FR-PROJ-005 — Project Roles

The platform shall support project-specific roles and permissions.

### FR-PROJ-006 — Project Health Summary

The platform shall provide a project-level health summary combining:

- Service health
- Device health
- Build status
- Test status
- Quality-gate status
- Deployment status
- Active alerts
- Open incidents

### FR-PROJ-007 — Project Search and Filtering

Users shall be able to search and filter projects by:

- Name
- Organisation
- Status
- Tag
- Health state
- Owner

---

# 5.2 Repository Integration Requirements

### FR-REPO-001 — Repository Registration

The platform shall allow authorised users to associate a source-code repository with a project.

### FR-REPO-002 — GitHub Integration

The initial supported source-control provider shall be GitHub.

### FR-REPO-003 — Repository Metadata

The platform shall store:

- Repository name
- Repository URL
- Provider
- Default branch
- Visibility
- Last synchronisation date
- Integration status

### FR-REPO-004 — Secure Credentials

Repository credentials and tokens shall never be stored in plain text.

### FR-REPO-005 — Webhook Registration

The platform shall support receiving repository webhook events.

### FR-REPO-006 — Webhook Signature Validation

Every supported webhook event shall be validated using a secure signature mechanism.

### FR-REPO-007 — Event History

The platform shall retain a searchable history of supported repository events.

### FR-REPO-008 — Commit Traceability

Builds, deployments and quality results should be traceable to:

- Commit identifier
- Branch
- Author
- Commit message
- Timestamp

---

# 5.3 Build and Automation Requirements

### FR-BUILD-001 — Build Definition

The platform shall support defining a build workflow for a registered project.

### FR-BUILD-002 — Build Trigger

An authorised build may be triggered through:

- Manual user action
- Repository webhook
- Approved scheduled execution
- Approved API request

### FR-BUILD-003 — Build Record

Every build shall produce a persistent record containing:

- Build identifier
- Project
- Repository
- Commit
- Branch
- Trigger source
- Start time
- End time
- Duration
- Status
- Logs
- Failure reason
- Triggering user or event

### FR-BUILD-004 — Build Status

Supported statuses shall include at minimum:

- Queued
- Running
- Successful
- Failed
- Cancelled
- Timed Out

### FR-BUILD-005 — Build Logs

The platform shall make build logs available to authorised users.

### FR-BUILD-006 — Build Cancellation

Authorised users shall be able to cancel eligible running builds.

### FR-BUILD-007 — Build Timeout

Build workflows shall support configurable timeout limits.

### FR-BUILD-008 — Build Isolation

Build execution shall be isolated from the main application runtime.

### FR-BUILD-009 — Build History

Users shall be able to search and filter build history.

### FR-BUILD-010 — Rebuild

Authorised users should be able to rerun a previous build using approved configuration.

---

# 5.4 Testing Requirements

### FR-TEST-001 — Automated Test Execution

The platform shall support execution or ingestion of automated test results.

### FR-TEST-002 — Test Result Storage

The platform shall store:

- Total tests
- Passed tests
- Failed tests
- Skipped tests
- Test duration
- Failure details
- Test framework
- Build identifier

### FR-TEST-003 — Test History

Users shall be able to view historical test trends.

### FR-TEST-004 — Failure Visibility

Failed tests shall display sufficient information for investigation without exposing secrets.

### FR-TEST-005 — Test Evidence

Test results shall be exportable or available for project evidence.

---

# 5.5 Code Quality Requirements

### FR-QUAL-001 — Code Analysis

The platform shall support code-quality analysis for approved project types.

### FR-QUAL-002 — Initial Language Scope

Initial implementation should prioritise technologies already used by EdgeCloud, including:

- Java
- Spring Boot
- JavaScript
- React
- Python

### FR-QUAL-003 — Coverage Ingestion

The platform shall support ingestion of test coverage reports, including JaCoCo for Java projects.

### FR-QUAL-004 — Quality Metrics

The platform should support:

- Test coverage
- Complexity
- Duplication indicators
- Code-smell indicators
- Reliability findings
- Security findings
- Maintainability indicators
- Technical-debt estimates

### FR-QUAL-005 — Quality Findings

Each finding shall include:

- Project
- Repository
- File
- Rule
- Severity
- Description
- Location
- Detection date
- Status

### FR-QUAL-006 — Quality Gate

The platform shall support configurable quality gates.

### FR-QUAL-007 — Quality-Gate Result

A quality-gate evaluation shall return:

- Passed
- Failed
- Warning
- Not Evaluated

### FR-QUAL-008 — Quality-Gate Explanation

The platform shall explain which conditions passed or failed.

### FR-QUAL-009 — Quality History

Users shall be able to compare quality results over time.

### FR-QUAL-010 — Incremental Replacement

The platform shall clearly distinguish between:

- Native analysis
- Imported analysis
- Planned analysis
- Unsupported analysis

---

# 5.6 Deployment Requirements

### FR-DEP-001 — Deployment Record

The platform shall record deployments associated with a project.

### FR-DEP-002 — Deployment Metadata

A deployment record shall include:

- Project
- Environment
- Version
- Commit
- Build
- Status
- Start time
- End time
- Initiating user
- Deployment method

### FR-DEP-003 — Environments

The platform shall support named environments such as:

- Development
- Test
- Staging
- Production

### FR-DEP-004 — Deployment Status

Supported statuses shall include:

- Pending
- Running
- Successful
- Failed
- Cancelled
- Rolled Back

### FR-DEP-005 — Deployment History

Users shall be able to review deployment history.

### FR-DEP-006 — Approval Gate

The platform should support approval before deployment to protected environments.

### FR-DEP-007 — Rollback Evidence

The platform shall record rollback activity even where rollback execution is handled externally.

### FR-DEP-008 — Deployment Traceability

A deployment shall be traceable to its:

- Project
- Repository
- Commit
- Build
- Quality-gate decision
- Environment

---

# 5.7 Microservice Observability Requirements

### FR-OBS-001 — Service Registration

The platform shall discover or register supported microservices.

### FR-OBS-002 — Project Association

Every monitored service should be associated with a project.

### FR-OBS-003 — Health Monitoring

The platform shall monitor service health.

### FR-OBS-004 — JVM Monitoring

For supported Java services, the platform should collect:

- Heap usage
- Non-heap usage
- Garbage-collection indicators
- Thread count
- CPU usage
- Process uptime

### FR-OBS-005 — API Availability

The platform shall support monitoring approved API endpoints.

### FR-OBS-006 — Response-Time Monitoring

The platform should capture response-time indicators for monitored endpoints.

### FR-OBS-007 — Error-Rate Monitoring

The platform should track supported service error-rate metrics.

### FR-OBS-008 — Dependency Visibility

The platform should display dependencies between monitored services.

### FR-OBS-009 — Historical Metrics

The platform shall store historical service metrics according to retention policies.

### FR-OBS-010 — Container Monitoring

The platform should support Docker container status and resource monitoring.

### FR-OBS-011 — Service Dashboard

Users shall be able to view a detailed service dashboard.

### FR-OBS-012 — Fault Tolerance

A failed monitored service shall not stop monitoring of other services.

---

# 5.8 Edge Device Requirements

### FR-EDGE-001 — Preserve Existing Device Registration

The existing Version 1.0 device registration workflow shall remain supported.

### FR-EDGE-002 — Preserve Existing Telemetry

The platform shall continue supporting:

- CPU usage
- Memory usage
- Temperature
- Heartbeats
- Device status
- Historical telemetry

### FR-EDGE-003 — Fleet View

The platform shall provide a fleet-level view of registered edge devices.

### FR-EDGE-004 — Device Groups

Authorised users should be able to organise devices into groups.

### FR-EDGE-005 — Project Association

Edge devices should be associable with a software project.

### FR-EDGE-006 — Offline Detection

The platform shall identify devices that stop sending expected heartbeats.

### FR-EDGE-007 — Device History

The platform shall retain device availability and health history.

### FR-EDGE-008 — Agent Version

The platform should store the installed edge-agent version.

### FR-EDGE-009 — Device Metadata

The platform should support metadata including:

- Hostname
- Device type
- Operating system
- Architecture
- Location label
- Environment
- Tags

### FR-EDGE-010 — Future Remote Configuration

The architecture shall allow future secure remote configuration without requiring it in the first release.

---

# 5.9 Alerting Requirements

### FR-ALERT-001 — Preserve Existing Alerts

Existing Version 1.0 threshold alerts shall remain operational.

### FR-ALERT-002 — Project-Aware Alerts

Alerts should be associated with a project where applicable.

### FR-ALERT-003 — Alert Rules

Authorised users shall be able to define alert rules.

### FR-ALERT-004 — Severity

Supported severity levels shall include:

- Informational
- Low
- Medium
- High
- Critical

### FR-ALERT-005 — Alert Sources

Alerts may originate from:

- Microservice metrics
- Edge-device telemetry
- Build failures
- Test failures
- Quality-gate failures
- Deployment failures
- Security findings
- Availability failures

### FR-ALERT-006 — Deduplication

The platform shall reduce duplicate alerts for the same active condition.

### FR-ALERT-007 — Acknowledgement

Authorised users shall be able to acknowledge alerts.

### FR-ALERT-008 — Resolution

Alerts shall support resolution status and timestamps.

### FR-ALERT-009 — Notification Channels

The platform should support configurable notification channels.

### FR-ALERT-010 — Escalation

Critical unacknowledged alerts should support escalation rules.

### FR-ALERT-011 — Alert History

Users shall be able to search alert history.

### FR-ALERT-012 — Alert Explanation

The platform shall explain the condition that caused an alert.

---

# 5.10 Incident Management Requirements

### FR-INC-001 — Incident Creation

The platform shall support creating an incident from one or more alerts.

### FR-INC-002 — Incident Status

Supported incident statuses shall include:

- Open
- Investigating
- Mitigated
- Resolved
- Closed

### FR-INC-003 — Incident Severity

Incidents shall have a defined severity.

### FR-INC-004 — Incident Ownership

An incident may be assigned to an authorised user or team.

### FR-INC-005 — Incident Timeline

The platform shall retain an incident timeline.

### FR-INC-006 — Related Evidence

Incidents should link to:

- Alerts
- Services
- Devices
- Builds
- Deployments
- Commits
- Quality-gate results

### FR-INC-007 — Resolution Summary

Resolved incidents shall support a resolution summary.

### FR-INC-008 — Root-Cause Notes

Users shall be able to record root-cause findings.

### FR-INC-009 — Incident Reporting

Incident details shall be exportable for review and reporting.

---

# 5.11 Analytics Requirements

### FR-AN-001 — Project Dashboard

The platform shall provide a project dashboard combining engineering and operational indicators.

### FR-AN-002 — Engineering Trends

The platform should display trends for:

- Build success rate
- Test success rate
- Coverage
- Quality-gate outcomes
- Deployment frequency
- Deployment failure rate
- Alert volume
- Incident volume
- Service availability

### FR-AN-003 — Reliability Indicators

The platform should calculate supported reliability indicators such as:

- Mean time to acknowledge
- Mean time to resolve
- Availability
- Failure frequency

### FR-AN-004 — DORA-Inspired Metrics

Where sufficient data exists, the platform may provide:

- Deployment frequency
- Lead time for changes
- Change failure rate
- Time to restore service

### FR-AN-005 — Data Explanation

Calculated metrics shall explain their data source and calculation.

### FR-AN-006 — Date Filtering

Analytics shall support filtering by approved date range.

### FR-AN-007 — Role-Aware Views

Dashboard content shall reflect the user’s role and permission level.

---

# 5.12 Reporting Requirements

### FR-REP-001 — Report Generation

Authorised users shall be able to generate reports.

### FR-REP-002 — Report Types

Initial report types should include:

- Project health report
- Build report
- Code-quality report
- Deployment report
- Alert report
- Incident report
- Edge-device report
- Student evidence report
- Management summary

### FR-REP-003 — Export Formats

Reports should support professional export formats such as PDF and CSV where appropriate.

### FR-REP-004 — Report Metadata

Reports shall include:

- Report title
- Project
- Date range
- Generated date
- Generated by
- Data sources
- Relevant limitations

### FR-REP-005 — Reproducibility

A generated report should be traceable to the underlying platform data.

---

# 5.13 Organisation and Tenant Requirements

### FR-TEN-001 — Organisation Creation

The platform shall support organisations.

### FR-TEN-002 — Organisation Membership

Users may belong to one or more approved organisations where permitted by the final access model.

### FR-TEN-003 — Tenant Isolation

Organisation-owned data shall be isolated from other organisations.

### FR-TEN-004 — Organisation Projects

Projects shall belong to an organisation or approved personal workspace.

### FR-TEN-005 — Organisation Roles

The platform shall support organisation-level roles.

### FR-TEN-006 — Cross-Tenant Protection

The platform shall block unauthorised cross-tenant access.

### FR-TEN-007 — Tenant-Aware Queries

All tenant-owned data queries shall enforce tenant scope.

---

# 5.14 User and Access Requirements

### FR-USER-001 — Authentication

The platform shall continue using secure authentication.

### FR-USER-002 — Role-Based Access

The platform shall enforce role-based access control.

### FR-USER-003 — Resource Ownership

Access decisions shall consider:

- Platform role
- Organisation membership
- Project membership
- Resource ownership
- Explicit permission

### FR-USER-004 — Session Security

Authentication tokens shall be protected and expire according to approved policy.

### FR-USER-005 — User Status

The platform shall support user status such as:

- Active
- Invited
- Suspended
- Disabled

### FR-USER-006 — Least Privilege

Users shall receive the minimum permissions required for their role.

---

# 5.15 Audit Requirements

### FR-AUD-001 — Audit Events

Security-sensitive and governance-sensitive actions shall be audited.

### FR-AUD-002 — Audit Details

Audit records should include:

- Actor
- Action
- Resource
- Timestamp
- Organisation
- Project
- Result
- Relevant metadata

### FR-AUD-003 — Audit Protection

Users shall not be able to silently modify audit history.

### FR-AUD-004 — Audit Search

Authorised users shall be able to search audit records.

### FR-AUD-005 — Audit Retention

Audit data shall follow a documented retention policy.

---

## 6. Non-Functional Requirements

# 6.1 Performance Requirements

### NFR-PERF-001

Common authenticated API requests should complete within an acceptable interactive response time under the defined test workload.

Target:

- 95% of standard read requests under 500 milliseconds in the local Docker reference environment, excluding external provider latency.

### NFR-PERF-002

Dashboard pages should avoid unnecessary repeated API calls.

### NFR-PERF-003

Large metric histories shall use pagination, aggregation or time-window limits.

### NFR-PERF-004

Build logs and analysis results shall support incremental loading where necessary.

---

# 6.2 Scalability Requirements

### NFR-SCALE-001

The architecture shall support horizontal growth of stateless services where practical.

### NFR-SCALE-002

Metric ingestion shall avoid blocking user-facing API operations.

### NFR-SCALE-003

High-volume records shall use suitable indexes.

### NFR-SCALE-004

Retention policies shall prevent unlimited telemetry and log growth.

### NFR-SCALE-005

The design shall not assume only one organisation, one project or one device.

---

# 6.3 Availability and Resilience Requirements

### NFR-RES-001

Failure of one monitored service shall not make the entire platform unavailable.

### NFR-RES-002

External integration failures shall be handled through:

- Timeouts
- Retries where safe
- Clear error status
- Failure logging
- Recovery strategy

### NFR-RES-003

The platform shall not lose existing Version 1.0 data through Version 2.0 upgrades without an approved migration.

### NFR-RES-004

Scheduled jobs shall prevent overlapping execution where overlap would cause inconsistency.

### NFR-RES-005

Critical background failures shall be observable.

---

# 6.4 Maintainability Requirements

### NFR-MAIN-001

Services shall maintain clear domain ownership.

### NFR-MAIN-002

Cross-service database access is prohibited.

### NFR-MAIN-003

Shared contracts shall be versioned where necessary.

### NFR-MAIN-004

New code shall follow documented coding and API standards.

### NFR-MAIN-005

Architecture decisions shall be documented.

### NFR-MAIN-006

Major components shall include automated tests.

---

# 6.5 Usability Requirements

### NFR-USE-001

The interface shall use modern, professional and responsive SaaS design patterns.

### NFR-USE-002

Technical failures shall be explained clearly.

### NFR-USE-003

Dashboards shall avoid overwhelming users with unprioritised metrics.

### NFR-USE-004

Role-specific views shall present relevant information.

### NFR-USE-005

Loading, empty, success and error states shall be designed intentionally.

### NFR-USE-006

Business-facing views shall avoid unnecessary technical terminology.

### NFR-USE-007

Student-facing views should explain pipeline and quality concepts where practical.

---

# 6.6 Compatibility Requirements

### NFR-COMP-001

The backend shall remain deployable through Docker Compose.

### NFR-COMP-002

The React dashboard shall support modern desktop browsers.

### NFR-COMP-003

The Raspberry Pi edge agent shall remain compatible with the supported Raspberry Pi environment.

### NFR-COMP-004

Version 2.0 APIs shall avoid unnecessary breaking changes to Version 1.0 clients.

### NFR-COMP-005

Database migrations shall be version-controlled.

---

# 6.7 Observability Requirements

### NFR-OBS-001

Version 2.0 services shall expose appropriate health information.

### NFR-OBS-002

Critical operations shall use structured logging.

### NFR-OBS-003

Sensitive data shall not appear in logs.

### NFR-OBS-004

Integration failures shall include traceable correlation identifiers where practical.

### NFR-OBS-005

Background jobs shall report execution status.

---

## 7. Security Requirements

### SEC-001 — Authentication Enforcement

Protected endpoints shall require valid authentication.

### SEC-002 — Authorisation Enforcement

Authorisation shall be enforced on the backend and not only in the frontend.

### SEC-003 — Tenant Isolation

All organisation-owned resources shall enforce tenant boundaries.

### SEC-004 — Secret Protection

The platform shall not store the following in plain text:

- Passwords
- Repository tokens
- Webhook secrets
- Deployment credentials
- API keys
- Private keys

### SEC-005 — Webhook Validation

External webhook requests shall be authenticated or cryptographically validated.

### SEC-006 — Input Validation

All externally supplied inputs shall be validated.

### SEC-007 — Injection Protection

The platform shall use safe persistence and command-execution practices.

### SEC-008 — Build Isolation

Untrusted project code shall not execute within the main application process.

### SEC-009 — Log Protection

Logs shall not expose secrets or sensitive credentials.

### SEC-010 — Audit Logging

Security-sensitive activity shall produce audit records.

### SEC-011 — Rate Limiting

High-risk or public endpoints should support rate limiting.

### SEC-012 — Error Handling

Error responses shall not expose stack traces or internal secrets in production.

### SEC-013 — Dependency Security

Dependencies shall be reviewed for known vulnerabilities.

### SEC-014 — Secure Defaults

New integrations shall default to disabled until explicitly configured.

### SEC-015 — File Validation

Uploaded reports, artefacts or configuration files shall be validated before processing.

### SEC-016 — Path Protection

Build, report and artefact storage shall prevent path traversal.

### SEC-017 — Command Protection

Build execution shall prevent unsafe command injection.

### SEC-018 — Access Revocation

Suspended or disabled users shall lose access according to approved policy.

---

## 8. Data Requirements

### DATA-001

Each microservice shall own its own database or schema according to the final architecture.

### DATA-002

Cross-service references shall use logical identifiers rather than database foreign keys across services.

### DATA-003

Primary identifiers should use UUIDs unless a documented exception is approved.

### DATA-004

Important state changes shall include timestamps.

### DATA-005

High-volume tables shall include suitable indexes.

### DATA-006

Telemetry, logs, build records and audit records shall have retention strategies.

### DATA-007

Deletion rules shall distinguish between:

- Active deletion
- Archiving
- Soft deletion
- Retention expiry
- Legal or audit preservation

### DATA-008

Sensitive integration data shall be encrypted or stored through an approved secret-management mechanism.

### DATA-009

Database migrations shall be repeatable and version-controlled.

### DATA-010

Backups and restoration shall be documented before production use.

---

## 9. API Requirements

### API-001

Version 2.0 APIs shall use consistent versioned routes.

Recommended pattern:

```text
/api/v1/...


API-002
REST APIs shall use appropriate HTTP methods and status codes.
API-003
Request and response DTOs shall be used instead of exposing persistence entities directly.
API-004
Validation errors shall use a consistent response structure.
API-005
List endpoints shall support pagination where data volume may grow.
API-006
Filtering and sorting shall use documented query parameters.
API-007
Protected APIs shall enforce role, organisation and project scope.
API-008
API documentation shall be maintained.
API-009
Breaking API changes shall require explicit review and migration planning.
API-010
External-provider callbacks shall use dedicated secured endpoints.
10. UI and UX Requirements
UI-001
The dashboard shall provide a clear global navigation structure.
UI-002
The product shall include project-oriented navigation.
UI-003
The user shall be able to move from a project summary to:
Repositories
Builds
Tests
Quality
Deployments
Services
Devices
Alerts
Incidents
Reports
Settings
UI-004
Dashboards shall use clear health and status indicators.
UI-005
Colour shall not be the only indicator of status.
UI-006
Tables shall support appropriate filtering, sorting and pagination.
UI-007
Destructive actions shall require confirmation.
UI-008
Permission-restricted actions shall be hidden or disabled appropriately, while backend enforcement remains mandatory.
UI-009
The interface shall provide professional empty states.
UI-010
The interface shall provide actionable error messages.
UI-011
The interface shall be responsive for common desktop and tablet layouts.
UI-012
Accessibility shall be considered in component design.
11. Integration Requirements
INT-001
GitHub shall be the first supported source-control integration.
INT-002
The integration architecture should allow additional providers later.
INT-003
Imported test and quality reports shall retain their original source type.
INT-004
External integration failures shall not corrupt existing platform data.
INT-005
Integration synchronisation status shall be visible.
INT-006
Provider-specific logic should be isolated behind a defined integration boundary.
INT-007
The platform shall distinguish clearly between:
Connected
Disconnected
Misconfigured
Unauthorised
Temporarily unavailable
12. Testing Requirements
TEST-001
Every implementation story shall define required test coverage.
TEST-002
Backend services shall include unit tests for business logic.
TEST-003
Repository and persistence changes shall include appropriate integration testing.
TEST-004
Security-sensitive endpoints shall include authorisation tests.
TEST-005
Tenant-owned data shall include cross-tenant access tests.
TEST-006
Frontend features shall include component or workflow validation where practical.
TEST-007
Critical workflows shall include end-to-end validation.
TEST-008
Version 1.0 regression tests shall confirm that Raspberry Pi and existing monitoring workflows remain operational.
TEST-009
Docker Compose validation shall be completed before release acceptance.
TEST-010
Testing evidence shall be recorded for completed Jira stories.
13. Documentation Requirements
DOC-001
Every major feature shall include technical documentation.
DOC-002
New APIs shall be documented.
DOC-003
New database structures shall be documented.
DOC-004
Architecture changes shall update the architecture documentation.
DOC-005
Configuration requirements shall be documented.
DOC-006
Testing evidence shall be stored professionally.
DOC-007
Known limitations shall be documented honestly.
DOC-008
User-facing workflows shall include suitable guidance.
DOC-009
Jira stories shall link to relevant documentation where practical.
DOC-010
Version 2.0 documentation shall remain separate from the completed Version 1.0 historical record.
14. Operational Requirements
OPS-001
The platform shall support Docker Compose deployment for development and demonstration.
OPS-002
Configuration shall use environment variables or approved external configuration.
OPS-003
Production secrets shall not be committed to Git.
OPS-004
Service startup order shall not depend on unsafe fixed delays where health checks can be used.
OPS-005
Container health checks should be defined for critical services.
OPS-006
Operational logs shall be accessible for diagnosis.
OPS-007
Database startup and readiness shall be handled safely.
OPS-008
Deployment documentation shall include startup, shutdown, validation and troubleshooting.
OPS-009
The system shall provide an operational health overview.
OPS-010
Rollback procedures shall be documented for significant releases.
15. Compliance and Governance Requirements
GOV-001
Role and permission changes shall be auditable.
GOV-002
Quality-gate policy changes shall be auditable.
GOV-003
Protected deployment approvals shall be auditable.
GOV-004
Organisation-level configuration changes shall be auditable.
GOV-005
Data-retention policies shall be documented.
GOV-006
The product shall identify where data originates.
GOV-007
Automated recommendations shall be distinguishable from verified facts.
GOV-008
Future AI features shall show supporting evidence and confidence where appropriate.
16. Version 1.0 Compatibility Requirements
COMP-V1-001
Existing authentication workflows shall remain functional unless replaced through a documented migration.
COMP-V1-002
Existing device registration shall remain functional.
COMP-V1-003
Existing Raspberry Pi telemetry shall remain functional.
COMP-V1-004
Existing heartbeat processing shall remain functional.
COMP-V1-005
Existing historical metric retrieval shall remain functional.
COMP-V1-006
Existing alert generation shall remain functional.
COMP-V1-007
Existing dashboard capabilities shall remain accessible during staged Version 2.0 development.
COMP-V1-008
Existing Docker Compose deployment shall remain available until a tested replacement is approved.
17. Initial Product Constraints
Version 2.0 development is constrained by:
Existing Spring Boot microservices
Existing React dashboard
Existing Docker Compose deployment
Existing MySQL service databases
Existing Raspberry Pi agent
Existing JWT security model
Limited initial development team size
Need for incremental delivery
Need to preserve the completed MSc baseline
Need for professional but achievable scope
These constraints must influence story sizing and architectural decisions.
18. Initial Assumptions
The current plan assumes:
GitHub is the first repository provider.
Docker Compose remains the primary deployment environment.
Java and React remain the main platform technologies.
Python remains suitable for the edge agent.
Existing services will be reused where domain ownership remains appropriate.
New services will only be created after architecture review.
Jenkins and SonarQube replacement will be incremental.
Raspberry Pi support will remain active.
Enterprise SaaS capability will begin with foundations rather than full commercial billing.
19. Product Exclusions
Unless separately approved, Version 2.0 does not require:
Complete Jenkins plugin compatibility
Complete SonarQube language compatibility
Kubernetes administration
Cloud infrastructure provisioning
Fully autonomous remediation
Automatic code modification
Multi-region production deployment
Enterprise billing
## 19. Product Exclusions

Unless separately approved, Version 2.0 does not require:

- Complete Jenkins plugin compatibility
- Complete SonarQube language compatibility
- Kubernetes administration
- Cloud infrastructure provisioning
- Fully autonomous remediation
- Automatic code modification
- Multi-region production deployment
- Enterprise billing
- Native mobile applications
- Every Git provider
- Every programming language
- Unlimited data retention
- Unrestricted execution of untrusted code

---

## 20. Definition of Product Readiness

The Version 2.0 requirements are ready to support architecture and Jira planning when:

- Functional requirements are reviewed.
- Non-functional requirements are measurable.
- Security requirements are accepted.
- Version 1.0 continuity is protected.
- Raspberry Pi requirements are preserved.
- Project, repository, build, quality, deployment, monitoring and alert domains are represented.
- Tenant and organisation requirements are included.
- Testing and documentation obligations are defined.
- Out-of-scope areas are clear.
- Major assumptions and constraints are understood.

---

## 21. Requirements Traceability

Every Jira story shall reference one or more requirement identifiers from this document.

Example:

Related Requirements:
- FR-PROJ-001
- FR-PROJ-006
- SEC-002
- TEST-002
- DOC-001

This traceability will connect:

Product Vision
    ↓
Product Requirements
    ↓
Platform Architecture
    ↓
Jira Epic
    ↓
Jira Story
    ↓
Implementation
    ↓
Testing Evidence
    ↓
Release Acceptance

---

## 22. Current Approval Status

**Status:** Draft

**Owner:** Taha Aflouk

**Version:** EdgeCloud Platform Version 2.0

**Previous document:** VERSION_2_PRODUCT_VISION.md

**Next document:** VERSION_2_PLATFORM_ARCHITECTURE.md
