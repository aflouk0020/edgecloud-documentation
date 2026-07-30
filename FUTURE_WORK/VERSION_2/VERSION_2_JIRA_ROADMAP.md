# EdgeCloud Platform Version 2.0 Jira Roadmap

## 1. Purpose

This document defines the Jira planning structure for EdgeCloud Platform Version 2.0.

It links:

- Release
- Epics
- Sprints
- Planned stories
- Dependencies
- Priorities
- Requirement traceability
- Delivery sequence

The roadmap must be reviewed before Sprint 7 implementation begins.

---

## 2. Release

**Release name:** EdgeCloud Monitor v2.0

**Product direction:** Engineering Operations Platform

**Status:** Planned

**Primary objective:** Extend the completed Version 1.0 monitoring platform into a unified system for observability, edge management, alerting, analytics, repository integration, quality management, CI/CD visibility and enterprise governance.

---

## 3. Epic Structure

| Epic | Primary Scope |
|---|---|
| Advanced Observability Platform | Projects, services, metrics, JVM monitoring and container visibility |
| Intelligent Alerting Platform | Rules, severity, acknowledgement, deduplication, escalation and incidents |
| Edge Device Management Platform | Raspberry Pi fleet visibility, grouping, history and device health |
| Analytics and Reporting Platform | Engineering dashboards, trends, reports and operational insight |
| DevOps and SaaS Platform | GitHub integration, builds, tests, quality gates and deployment tracking |
| Enterprise Platform | Organisations, teams, permissions, tenant isolation and governance |

---

## 4. Sprint Structure

| Sprint | Epic | Sprint Goal |
|---|---|---|
| Sprint 7 | Advanced Observability Platform | Establish project and observability foundations |
| Sprint 8 | Intelligent Alerting Platform | Improve alert detection, acknowledgement and incident response |
| Sprint 9 | Edge Device Management Platform | Extend Raspberry Pi monitoring into fleet management |
| Sprint 10 | Analytics and Reporting Platform | Convert platform data into professional insight and reports |
| Sprint 11 | DevOps and SaaS Platform | Introduce repository, build, testing and quality capabilities |
| Sprint 12 | Enterprise Platform | Introduce organisation, permission and tenant foundations |

---


---

## 5. Story Identification Standard

All Version 2.0 stories must use the existing Jira project key.

Example story identifier:

SCRUM-201

Story numbers are assigned by Jira and must not be predicted manually.

Each story should include:

- Epic
- Sprint
- Fix Version
- Priority
- Story Points
- Component
- Labels
- Requirement References
- Dependencies
- Acceptance Criteria
- Definition of Done
- Testing Requirements
- Documentation Requirements

---

## 6. Sprint 7 – Advanced Observability Platform

### Goal

Establish the project-oriented observability foundation.

Planned work:

- Software Project Registration
- Project Search
- Project Details
- Project Health Summary
- Associate Services with Projects
- Associate Devices with Projects
- JVM Metrics
- API Availability Monitoring
- Docker Container Visibility
- Observability Dashboard
- Sprint Review

---

## 7. Sprint 8 – Intelligent Alerting Platform

### Goal

Improve alerting through acknowledgement, escalation and incident support.

Planned work:

- Project Alert Rules
- Alert Severity
- Alert Deduplication
- Alert Acknowledgement
- Alert Resolution
- Notification Channels
- Escalation
- Alert History
- Incident Management
- Sprint Review

---

## 8. Sprint 9 – Edge Device Management Platform

### Goal

Expand Raspberry Pi monitoring into fleet management.

Planned work:

- Fleet View
- Device Groups
- Device Metadata
- Availability History
- Offline Detection
- Agent Versions
- Device Health
- Device Tags
- Project Device View
- Sprint Review

---

## 9. Sprint 10 – Analytics and Reporting Platform

### Goal

Provide engineering dashboards and reporting.

Planned work:

- Engineering Analytics
- Project Health Dashboard
- Availability Trends
- Alert Trends
- Reliability Metrics
- Management Dashboard
- PDF Reports
- CSV Export
- Sprint Review

---

## 10. Sprint 11 – DevOps Platform

### Goal

Introduce repository integration and engineering visibility.

Planned work:

- Repository Registration
- GitHub Integration
- Webhooks
- Build Records
- Test Results
- Coverage Import
- Quality Findings
- Quality Gates
- Deployment History
- Sprint Review

---

## 11. Sprint 12 – Enterprise Platform

### Goal

Introduce organisations, governance and tenant support.

Planned work:

- Organisations
- Teams
- Membership
- Permissions
- Tenant Isolation
- Audit Logging
- Administration
- Retention Policies
- Release Review

---

## 12. Story Priority

| Priority | Meaning |
| --- | --- |
| Highest | Critical dependency or security |
| High | Required for sprint success |
| Medium | Important but movable |
| Low | Improvement or enhancement |

---

## 13. Story Point Guidance

| Points | Typical Size |
| --- | --- |
| 1 | Very small |
| 2 | Small |
| 3 | Standard |
| 5 | Medium feature |
| 8 | Complex feature |
| 13 | Should normally be split |

---

## 14. Dependency Rules

Every story should identify:

- Blocking stories
- Blocked stories
- Service dependencies
- Data dependencies
- Security dependencies
- Documentation dependencies

---

## 15. Definition of Ready

A story is ready when:

- Business value is clear.
- Acceptance criteria are testable.
- Requirements are referenced.
- Dependencies are identified.
- Security has been considered.
- Story points are assigned.
- Sprint and Epic are selected.
- Definition of Done is included.

---

## 16. Release Readiness

Version 2.0 is ready for release review when:

- Required stories are complete.
- Builds pass.
- Security tests pass.
- Regression tests pass.
- Raspberry Pi workflows remain operational.
- Documentation is complete.
- Rollback procedures exist.

---

## 17. Current Status

**Status:** Draft

**Owner:** Taha Aflouk

**Version:** EdgeCloud Platform Version 2.0

**Previous document:** VERSION_2_PLATFORM_ARCHITECTURE.md

**Next document:** VERSION_2_STORY_STANDARD.md

