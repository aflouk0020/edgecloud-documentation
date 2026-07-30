# EdgeCloud Platform Version 2.0 Dependency Matrix

## 1. Purpose

This document records the main dependencies between Version 2.0 sprints, services, capabilities and external integrations.

The purpose is to:

- Identify blocking work
- Protect sprint sequencing
- Reduce integration risk
- Clarify service ownership
- Support Jira planning
- Improve release readiness

---

## 2. Dependency Principles

All dependencies must be:

- Explicit
- Traceable
- Reviewed before sprint entry
- Linked to Jira stories where relevant
- Reassessed when architecture changes

A story must not begin when a critical dependency is unresolved.

---

## 3. Sprint Dependency Matrix

| Sprint | Depends On | Provides Foundation For |
| --- | --- | --- |
| Sprint 7 | Version 1.0 services | Sprints 8 to 12 |
| Sprint 8 | Sprint 7 project model and monitoring data | Sprint 10 analytics and incident reporting |
| Sprint 9 | Sprint 7 project model and Sprint 8 alert improvements | Sprint 10 reporting |
| Sprint 10 | Sprints 7 to 9 operational data | Sprint 12 enterprise dashboards |
| Sprint 11 | Sprint 7 projects and secure integration design | Sprint 12 governance and audit |
| Sprint 12 | All previous sprints | Version 2.0 release readiness |

---

## 4. Service Dependency Matrix

| Service or Capability | Primary Dependencies |
| --- | --- |
| API Gateway | Discovery Service, Authentication Service |
| Authentication Service | User database, security configuration |
| Project Service | Authentication Service, API Gateway |
| Monitoring Service | Device Service, registered services |
| Device Service | Raspberry Pi agent, Project Service |
| Alert Service | Monitoring Service, Device Service, Project Service |
| Integration Service | Project Service, GitHub, webhook security |
| Quality Service | Build results, test reports, repository metadata |
| Analytics Service | Project, monitoring, alert, incident and quality data |
| Build Runner | Build control capability, container runtime |
| Reporting Capability | Analytics Service, export libraries |
| Organisation Capability | Authentication Service, Project Service |

---

## 5. Data Dependencies

| Data | Owner | Main Consumers |
| --- | --- | --- |
| User identity | Authentication Service | All protected services |
| Project data | Project Service | Monitoring, Device, Alert, Integration, Analytics |
| Repository data | Integration Service | Build, Quality, Analytics |
| Build data | DevOps capability | Quality, Deployment, Analytics |
| Test data | Quality or DevOps capability | Analytics, Reporting |
| Quality findings | Quality Service | Project dashboard, Analytics |
| Deployment data | DevOps capability | Monitoring, Analytics |
| Runtime metrics | Monitoring Service | Alert Service, Analytics |
| Device metadata | Device Service | Monitoring, Alert, Analytics |
| Alert data | Alert Service | Incident, Analytics, Reporting |
| Organisation data | Organisation capability | Authentication, Project, Audit |

---

## 6. External Dependencies

| Dependency | Purpose | Risk |
| --- | --- | --- |
| GitHub API | Repository integration | Availability and rate limits |
| GitHub Webhooks | Repository events | Signature and replay security |
| Docker Engine | Build and deployment execution | Resource and isolation risks |
| Raspberry Pi | Edge validation | Hardware availability |
| Maven | Backend builds | Dependency availability |
| npm | Frontend builds | Package compatibility |
| PDF library | Report generation | Layout and compatibility |
| Database engine | Service persistence | Migration and availability |

---

## 7. Security Dependencies

| Capability | Required Security Dependency |
| --- | --- |
| Protected APIs | Valid JWT and backend authorisation |
| Project access | Project membership and role checks |
| Tenant access | Organisation-aware authorisation |
| GitHub webhooks | Signature verification |
| Build execution | Isolated runner and resource limits |
| Secrets | Environment or approved secret storage |
| Reports | Authorised data scope |
| Audit search | Restricted administrative access |

---

## 8. Infrastructure Dependencies

Version 2.0 depends on:

- Docker Compose
- Internal Docker networking
- Service discovery
- API Gateway routing
- Service-owned databases
- Environment configuration
- Health checks
- Persistent volumes where required

New services must not be added to Docker Compose until their configuration and health behaviour are defined.

---

## 9. Critical Path

The current critical path is:

1. Preserve Version 1.0 stability.
2. Implement Project Service.
3. Associate services and devices with projects.
4. Extend observability.
5. Improve alerts and incidents.
6. Create analytics read models.
7. Add repository and build capabilities.
8. Introduce enterprise scope and audit.
9. Complete release validation.

The Project Service is the most important new dependency for Version 2.0.

---

## 10. Dependency Review Checklist

Before starting a story, confirm:

- Blocking stories are complete.
- Required APIs exist.
- Required data is available.
- Service ownership is clear.
- Security controls are defined.
- Infrastructure is available.
- External integration access is available.
- Migration requirements are understood.
- Documentation dependencies are identified.
- Test environments are ready.

---

## 11. Dependency Status Values

| Status | Meaning |
| --- | --- |
| Not Started | Dependency work has not begun |
| In Progress | Dependency is being implemented |
| Available | Dependency is ready for use |
| Blocked | Dependency cannot proceed |
| At Risk | Dependency may affect delivery |
| Removed | Dependency is no longer required |

Jira stories should use links and comments to reflect significant dependency changes.

---

## 12. Current Status

**Status:** Draft

**Owner:** Taha Aflouk

**Version:** EdgeCloud Platform Version 2.0

**Previous document:** VERSION_2_RISK_ASSESSMENT.md

**Next document:** VERSION_2_DATABASE_PLAN.md
