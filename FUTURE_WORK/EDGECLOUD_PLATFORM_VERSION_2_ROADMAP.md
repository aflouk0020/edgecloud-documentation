Excellent. Now we can formally define **EdgeCloud Platform Version 2.0** without disturbing the completed Version 1.0 baseline.

The immediate task is not coding. It is to create the **product roadmap, architecture direction, epic structure and Jira backlog** for Version 2.0.

# 1. Freeze Version 1.0

Version 1.0 should now be treated as a completed release:

```text
EdgeCloud Monitor Version 1.0
Cloud-Native Monitoring and Edge Telemetry Platform
```

It includes:

- Discovery Service
- API Gateway
- Authentication Service
- Monitoring Service
- Device Service
- Alert Service
- React dashboard
- Raspberry Pi edge agent
- Docker Compose deployment
- Historical metrics
- Threshold-based alerts
- Testing and documentation

Do not reorganise Sprints 1–6 or rewrite their history. Future development should extend the platform through new services, APIs and database migrations while maintaining backward compatibility.

---

# 2. Create the Version 2.0 future-work document

Use:

```text
Documentation/FUTURE_WORK/EDGECLOUD_PLATFORM_VERSION_2_ROADMAP.md
```

This should become the authoritative roadmap for Version 2.0.

I recommend using this name instead of `POST_MVP_FUTURE_WORK_PLAN.md` because Version 1.0 is no longer merely an MVP. It is a completed platform release.

Recommended structure:

```markdown
# EdgeCloud Platform Version 2.0 Roadmap

## 1. Document Purpose

## 2. Version 1.0 Baseline

## 3. Product Vision

## 4. Target Users

## 5. Product Problems Addressed

## 6. Version 2.0 Objectives

## 7. Scope

## 8. Non-Goals

## 9. Product Principles

## 10. Epic Roadmap

## 11. Sprint Roadmap

## 12. Proposed Architecture Evolution

## 13. Security and Multi-Tenancy Strategy

## 14. Edge and Raspberry Pi Continuity

## 15. Notification Strategy

## 16. Risks and Constraints

## 17. Success Metrics

## 18. Release Strategy

## 19. Version 3.0 Opportunities
```

---

# 3. Version 2.0 product identity

## Current identity

```text
EdgeCloud Monitor
Cloud-Native Monitoring and Edge Telemetry Platform
```

## Version 2.0 identity

```text
EdgeCloud Platform
Engineering Operations, Observability and Edge Management SaaS
```

The platform will connect five operational areas:

```text
Software Services
        +
CI/CD Pipelines
        +
Code Quality
        +
Incidents and Notifications
        +
Raspberry Pi and Edge Devices
```

The goal is not to claim that Version 2.0 immediately replaces Jenkins, SonarQube, Datadog or Grafana.

The realistic goal is:

> Provide smaller teams with a unified, lightweight platform for service monitoring, edge telemetry, software delivery visibility, engineering quality and incident response.

That is commercially credible and technically achievable.

---

# 4. Target users

Version 2.0 should be designed for:

- Small software engineering teams
- Start-ups
- University development teams
- DevOps engineers
- Software developers
- System administrators
- IoT and edge-computing teams
- Organisations managing Raspberry Pi fleets
- Technical managers requiring engineering metrics

---

# 5. Main product domains

Version 2.0 should be divided into six product domains.

```text
1. Software Delivery
2. Code Quality
3. Engineering Intelligence
4. Incident Management
5. SaaS Governance
6. Intelligent Operations
```

The current monitoring and edge capabilities remain underneath all six.

---

# 6. Version 2.0 roadmap

Version 2.0 requires **six additional sprints**:

| Sprint | Product Area | Main Outcome |
|---|---|---|
| Sprint 7 | Repository and CI/CD Integration | EdgeCloud understands builds, commits and deployments |
| Sprint 8 | Code Quality Platform | EdgeCloud reports software quality and quality gates |
| Sprint 9 | Engineering Intelligence | EdgeCloud calculates delivery and reliability metrics |
| Sprint 10 | Incident Management | Alerts become structured operational incidents |
| Sprint 11 | SaaS Foundation | Organisations and teams can securely use the platform |
| Sprint 12 | Intelligent Operations | Anomaly detection and assisted troubleshooting |

These should be created in Jira as future sprints, but only Sprint 7 should become active when implementation begins.

---

# 7. Epic structure

Create six new Jira epics.

## Epic 4 — Repository and Delivery Intelligence

```text
Epic name:
Repository and Delivery Intelligence

Version:
2.0

Sprints:
Sprint 7
```

Purpose:

Connect EdgeCloud to source-control and delivery systems so monitoring events can be correlated with commits, builds, releases and deployments.

---

## Epic 5 — Software Quality Intelligence

```text
Epic name:
Software Quality Intelligence

Version:
2.0

Sprints:
Sprint 8
```

Purpose:

Provide code-quality, testing and security indicators for connected repositories.

---

## Epic 6 — Engineering Performance Intelligence

```text
Epic name:
Engineering Performance Intelligence

Version:
2.0

Sprints:
Sprint 9
```

Purpose:

Transform operational and deployment data into reliability and delivery metrics.

---

## Epic 7 — Incident and Reliability Operations

```text
Epic name:
Incident and Reliability Operations

Version:
2.0

Sprints:
Sprint 10
```

Purpose:

Manage the complete lifecycle from alert generation to acknowledgement, investigation and recovery.

---

## Epic 8 — Multi-Tenant SaaS Platform

```text
Epic name:
Multi-Tenant SaaS Platform

Version:
2.0

Sprints:
Sprint 11
```

Purpose:

Allow multiple organisations and teams to securely use EdgeCloud.

---

## Epic 9 — Intelligent Operations

```text
Epic name:
Intelligent Operations

Version:
2.0

Sprints:
Sprint 12
```

Purpose:

Introduce anomaly detection, correlation and decision support based on platform telemetry.

---

# 8. Sprint 7 — Repository and CI/CD Integration

## Sprint goal

> Enable users to connect GitHub repositories and view software delivery activity alongside operational monitoring data.

## Recommended stories

### EC2-001 — Repository Integration Architecture

As a platform architect, I want to define the repository integration architecture so that external source-control providers can be integrated securely and consistently.

Acceptance criteria:

- GitHub is selected as the first supported provider.
- Provider-specific logic is separated from core domain logic.
- Webhook, authentication and data-flow architecture is documented.
- No Version 1.0 service is directly coupled to GitHub-specific payloads.
- Security risks and secret-management requirements are documented.

---

### EC2-002 — Repository Registration

As an administrator, I want to register a repository so that EdgeCloud can associate software delivery events with a monitored system.

Fields:

- Repository name
- Provider
- Repository owner
- Repository URL
- Default branch
- Active status
- Associated project
- Webhook status

---

### EC2-003 — GitHub Webhook Receiver

As the platform, I want to receive verified GitHub webhook events so that repository activity can be processed automatically.

Supported initial events:

- Push
- Pull request
- Workflow run
- Release
- Deployment

Security requirements:

- Validate webhook signatures.
- Reject invalid signatures.
- Store delivery identifiers for idempotency.
- Prevent duplicate event processing.
- Never expose webhook secrets in logs.

---

### EC2-004 — Commit Activity History

As a developer, I want to view recent commit activity so that I can relate code changes to platform behaviour.

---

### EC2-005 — Build and Workflow History

As a developer, I want to view workflow execution history so that I can identify successful and failed builds.

Statuses:

```text
QUEUED
IN_PROGRESS
SUCCESS
FAILED
CANCELLED
SKIPPED
```

---

### EC2-006 — Deployment History

As an operator, I want to view deployments so that I can identify when operational changes entered an environment.

Suggested fields:

- Deployment ID
- Repository
- Environment
- Commit SHA
- Branch
- Deployment status
- Started time
- Completed time
- Triggered by
- Release version

---

### EC2-007 — Build Failure Alerts

As an operator, I want EdgeCloud to create an alert when a critical build fails so that the team can respond quickly.

This should reuse the existing Alert Service instead of creating a second notification system.

---

### EC2-008 — Delivery Activity Dashboard

As a user, I want a delivery dashboard so that I can see repository, build and deployment health in one place.

Dashboard sections:

- Connected repositories
- Latest builds
- Failed builds
- Recent deployments
- Deployment success rate
- Latest release
- Build duration trends

---

### EC2-009 — Repository Integration Audit Events

As an administrator, I want repository configuration changes recorded so that integration activity is traceable.

---

### EC2-010 — Sprint 7 Integration Testing and Documentation

As a developer, I want the repository workflow tested and documented so that the implementation is reliable and repeatable.

---

# 9. Sprint 8 — Software Quality Intelligence

## Sprint goal

> Provide understandable and actionable software quality information for connected repositories.

Recommended stories:

```text
EC2-011 Quality Analysis Architecture
EC2-012 Quality Analysis Run Model
EC2-013 Test Coverage Import
EC2-014 Complexity Metrics
EC2-015 Technical Debt Indicators
EC2-016 Security Finding Import
EC2-017 Duplicate Code Indicators
EC2-018 Quality Gate Configuration
EC2-019 Repository Quality Score
EC2-020 Quality Trends Dashboard
EC2-021 Branch and Release Comparison
EC2-022 Quality Gate Failure Alerts
EC2-023 Sprint 8 Testing and Documentation
```

Important architectural decision:

Do not initially build a complete static-analysis engine from scratch.

Version 2.0 can support:

- JaCoCo report ingestion
- Maven test-result ingestion
- SARIF security-result ingestion
- Existing scanner integration
- Lightweight internal scoring

Later versions can implement deeper native analysis.

---

# 10. Sprint 9 — Engineering Intelligence

## Sprint goal

> Turn monitoring, incident and delivery data into engineering performance insights.

Recommended stories:

```text
EC2-024 Engineering Metrics Data Model
EC2-025 Deployment Frequency
EC2-026 Lead Time for Changes
EC2-027 Change Failure Rate
EC2-028 Mean Time to Recovery
EC2-029 Mean Time Between Failures
EC2-030 Service Availability and SLA
EC2-031 Release Reliability Score
EC2-032 Engineering Trends Dashboard
EC2-033 Executive Summary Dashboard
EC2-034 Metrics Export
EC2-035 Sprint 9 Testing and Documentation
```

These metrics should be computed from real platform records rather than manually entered values.

---

# 11. Sprint 10 — Incident Management

## Sprint goal

> Transform alerts into traceable incidents with ownership, timelines, recovery information and notifications.

Recommended stories:

```text
EC2-036 Incident Domain Architecture
EC2-037 Automatic Incident Creation
EC2-038 Manual Incident Creation
EC2-039 Incident Acknowledgement
EC2-040 Incident Assignment
EC2-041 Incident Status Lifecycle
EC2-042 Incident Timeline
EC2-043 Alert-to-Incident Correlation
EC2-044 Maintenance Windows
EC2-045 Root-Cause Recording
EC2-046 Recovery Tracking
EC2-047 Incident Notification Rules
EC2-048 Internal Service Status Page
EC2-049 Incident Dashboard
EC2-050 Sprint 10 Testing and Documentation
```

Recommended lifecycle:

```text
OPEN
ACKNOWLEDGED
INVESTIGATING
MITIGATED
RESOLVED
CLOSED
```

---

# 12. Sprint 11 — Multi-Tenant SaaS Foundation

## Sprint goal

> Allow multiple organisations to securely operate separate EdgeCloud workspaces.

Recommended stories:

```text
EC2-051 Tenant Architecture Review
EC2-052 Organisation Management
EC2-053 Workspace and Project Management
EC2-054 Team Management
EC2-055 User Invitations
EC2-056 Tenant-Aware RBAC
EC2-057 Tenant Data Isolation
EC2-058 API Key Management
EC2-059 Audit Log Platform
EC2-060 Subscription Plan Model
EC2-061 Usage Limits and Entitlements
EC2-062 Organisation Settings
EC2-063 SaaS Administration Dashboard
EC2-064 Tenant Security Testing
EC2-065 Sprint 11 Documentation
```

Do not add billing before tenant boundaries, permissions and data isolation are proven.

Security must come before subscriptions.

---

# 13. Sprint 12 — Intelligent Operations

## Sprint goal

> Provide intelligent detection, correlation and troubleshooting assistance using EdgeCloud operational data.

Recommended stories:

```text
EC2-066 Anomaly Detection Architecture
EC2-067 Telemetry Baseline Calculation
EC2-068 Metric Anomaly Detection
EC2-069 Predictive Threshold Alerts
EC2-070 Alert Correlation
EC2-071 Deployment-to-Incident Correlation
EC2-072 Root-Cause Suggestions
EC2-073 Capacity Forecasting
EC2-074 Automated Incident Summaries
EC2-075 Service Behaviour Analysis
EC2-076 Natural-Language Operational Search
EC2-077 AI Troubleshooting Assistant
EC2-078 AI Confidence and Evidence Display
EC2-079 AI Safety and Data Governance
EC2-080 Sprint 12 Testing and Documentation
```

Every AI recommendation should show:

- Supporting metrics
- Relevant events
- Confidence level
- Time window
- Affected service or device
- Whether the output is an observation, prediction or suggestion

The platform must never present an uncertain AI suggestion as a confirmed root cause.

---

# 14. Raspberry Pi and edge-device continuity

The Raspberry Pi must remain a core differentiator throughout Version 2.0.

It should integrate with the new features as follows:

## Sprint 7

- Edge-agent releases can be associated with repository releases.
- Agent deployment versions can be tracked.
- Failed edge-agent builds can generate alerts.

## Sprint 9

- Device availability contributes to reliability metrics.
- Fleet uptime and offline duration are measured.
- MTTR can include edge-device recovery.

## Sprint 10

- Device disconnection can automatically create incidents.
- Telemetry loss can appear on incident timelines.
- Device recovery resolves or mitigates incidents.

## Sprint 11

- Devices belong to an organisation and project.
- Tenant isolation applies to all telemetry.
- Organisation roles control device access.

## Sprint 12

- Abnormal CPU, memory or temperature behaviour can be detected.
- Repeated heartbeat failure can be predicted.
- Device failure patterns can be correlated.

Advanced fleet management should remain a Version 3.0 concern unless it becomes necessary earlier.

---

# 15. Notification architecture

The existing Alert Service should evolve into a broader notification and alerting platform.

Initial supported notifications:

- Dashboard
- Email
- Webhook

Future channels:

- Slack
- Microsoft Teams
- Telegram
- SMS
- Mobile push

Example conditions:

```text
Service becomes unavailable
Raspberry Pi misses heartbeat
CPU remains above threshold
Temperature becomes unsafe
Build fails
Deployment fails
Quality gate fails
Incident is created
Incident is escalated
Subscription usage approaches limit
AI detects abnormal behaviour
```

Version 2.0 should have notification preferences, severity levels, deduplication and cooldown periods.

---

# 16. Architecture evolution

Do not automatically create one microservice for every feature.

Begin with domain boundaries.

Potential new services:

```text
edgecloud-integration-service
edgecloud-quality-service
edgecloud-incident-service
edgecloud-organisation-service
edgecloud-intelligence-service
edgecloud-notification-service
```

Recommended initial order:

```text
Sprint 7:
Integration Service

Sprint 8:
Quality Service

Sprint 9:
Intelligence module or Engineering Metrics Service

Sprint 10:
Incident Service

Sprint 11:
Organisation Service

Sprint 12:
Intelligence Service expansion
```

The exact service boundaries should be confirmed through an architecture review before implementation.

---

# 17. Documentation structure for Version 2.0

Add:

```text
Documentation/
└── FUTURE_WORK/
    ├── EDGECLOUD_PLATFORM_VERSION_2_ROADMAP.md
    ├── VERSION_2_PRODUCT_VISION.md
    ├── VERSION_2_ARCHITECTURE_EVOLUTION.md
    ├── VERSION_2_EPIC_AND_SPRINT_PLAN.md
    ├── VERSION_2_SECURITY_AND_TENANCY_PLAN.md
    └── VERSION_3_OPPORTUNITIES.md
```

Later, when Sprint 7 starts, create:

```text
Documentation/
└── VERSION_2/
    ├── ARCHITECTURE/
    ├── API_DOCUMENTATION/
    ├── DATABASE_DESIGN/
    ├── DEPLOYMENT/
    ├── TESTING/
    ├── REPORTS/
    └── SPRINTS/
```

Do not mix Version 2.0 implementation evidence into completed Version 1.0 reports.

---

# 18. Jira setup order

Use this exact sequence:

1. Create release/version:

```text
EdgeCloud Platform 2.0
```

2. Create the six epics.

3. Create Sprints 7–12.

4. Create all stories in the backlog.

5. Link every story to its epic.

6. Add dependencies using “blocks” and “is blocked by”.

7. Add labels:

```text
version-2
saas
observability
edge
security
integration
backend
frontend
documentation
testing
```

8. Keep all stories in Backlog.

9. Select only Sprint 7 stories when implementation begins.

10. Do not start multiple Version 2.0 sprints simultaneously.

---

# 19. Definition of Ready

A Version 2.0 story should not enter a sprint unless it has:

- Clear user value
- Acceptance criteria
- Identified dependencies
- Security considerations
- API impact
- Database impact
- Frontend impact
- Testing requirements
- Documentation requirements
- Evidence requirements
- Estimated complexity

---

# 20. Definition of Done

Every Version 2.0 story should require:

- Implementation completed
- Unit tests passing
- Integration tests passing where applicable
- Security validation completed
- API documentation updated
- Database migration documented
- Frontend states completed
- Docker environment validated
- Screenshots or test evidence collected
- Jira acceptance criteria verified
- Pull request reviewed and merged
- Main branch remains healthy
- No Version 1.0 regression

---

# Immediate next action

The first planning task should be:

```text
Create:
FUTURE_WORK/EDGECLOUD_PLATFORM_VERSION_2_ROADMAP.md
```

Then complete these in order:

```text
1. VERSION_2_PRODUCT_VISION.md
2. VERSION_2_ARCHITECTURE_EVOLUTION.md
3. VERSION_2_EPIC_AND_SPRINT_PLAN.md
4. VERSION_2_SECURITY_AND_TENANCY_PLAN.md
5. Create Jira Version 2.0
6. Create Epics 4–9
7. Create Sprint 7 stories in full detail
8. Create outline stories for Sprints 8–12
9. Review dependencies
10. Begin Sprint 7 only after architecture approval
```

This gives EdgeCloud the same serious product discipline we use for MotoHub: a stable released baseline, a governed product roadmap, explicit security boundaries, controlled architecture evolution and incremental implementation.
