# EdgeCloud Platform Version 2.0 Risk Assessment

## 1. Purpose

This document identifies the main risks associated with EdgeCloud Platform Version 2.0.

It supports:

- Architecture planning
- Jira prioritisation
- Security review
- Sprint planning
- Release readiness
- Operational decision-making

The objective is to identify risks early, define practical controls and reduce avoidable delivery failures.

---

## 2. Risk Assessment Method

Each risk is assessed using:

- Likelihood
- Impact
- Overall rating
- Mitigation
- Owner
- Review point

### Likelihood

| Level | Meaning |
| --- | --- |
| Low | Unlikely to occur |
| Medium | May occur |
| High | Likely to occur |

### Impact

| Level | Meaning |
| --- | --- |
| Low | Limited disruption |
| Medium | Significant but manageable |
| High | Major technical, security or delivery impact |

### Overall Rating

| Rating | Action |
| --- | --- |
| Low | Monitor |
| Medium | Mitigate and review |
| High | Immediate control required |

---

## 3. Technical Risks

| ID | Risk | Likelihood | Impact | Rating | Mitigation |
| --- | --- | --- | --- | --- | --- |
| R-T01 | Excessive microservice fragmentation | Medium | High | High | Introduce new services only when domain boundaries justify separation |
| R-T02 | Tight coupling between services | Medium | High | High | Use clear APIs, logical identifiers and event-based integration where suitable |
| R-T03 | Version 2.0 changes break Version 1.0 workflows | Medium | High | High | Preserve existing APIs, add regression tests and use incremental migration |
| R-T04 | Monitoring data grows without control | High | High | High | Add retention, aggregation, pagination and archiving policies |
| R-T05 | Cross-domain analytics becomes too complex | Medium | Medium | Medium | Use dedicated read models and avoid direct cross-database access |
| R-T06 | Build runner affects platform stability | Medium | High | High | Isolate build execution in separate containers with limits and timeouts |
| R-T07 | External integrations become unreliable | Medium | Medium | Medium | Add retries, timeouts, failure states and integration health monitoring |
| R-T08 | Docker Compose becomes difficult to maintain | Medium | Medium | Medium | Keep services documented, use health checks and control environment configuration |

---

## 4. Security Risks

| ID | Risk | Likelihood | Impact | Rating | Mitigation |
| --- | --- | --- | --- | --- | --- |
| R-S01 | Unauthorised cross-project access | Medium | High | High | Enforce project scope in backend services and security tests |
| R-S02 | Weak tenant isolation | Medium | High | High | Add organisation-aware authorisation and cross-tenant tests |
| R-S03 | Webhook spoofing | Medium | High | High | Validate signatures, timestamps and replay attempts |
| R-S04 | Secrets committed to source control | Medium | High | High | Use environment variables, secret scanning and review checks |
| R-S05 | Untrusted repository code escapes isolation | Low | High | High | Restrict build runners, network access, permissions and execution time |
| R-S06 | Sensitive data appears in logs | Medium | Medium | Medium | Apply logging standards and review error output |
| R-S07 | Frontend-only authorisation creates exposure | Medium | High | High | Enforce all access rules in backend services |
| R-S08 | Excessive user privileges | Medium | High | High | Apply least privilege and role-aware access control |

---

## 5. Operational Risks

| ID | Risk | Likelihood | Impact | Rating | Mitigation |
| --- | --- | --- | --- | --- | --- |
| R-O01 | Service failure is not detected quickly | Medium | High | High | Add health checks, availability monitoring and alerts |
| R-O02 | Alert flooding reduces usefulness | High | Medium | High | Add deduplication, severity, acknowledgement and suppression |
| R-O03 | Raspberry Pi agents become outdated | Medium | Medium | Medium | Record agent versions and provide compatibility guidance |
| R-O04 | Database migration causes data loss | Low | High | High | Use backups, migration scripts, testing and rollback plans |
| R-O05 | Deployment state is unclear | Medium | Medium | Medium | Record deployment history, status and evidence |
| R-O06 | Generated reports are inaccurate | Low | High | Medium | Generate reports from approved data sources and add validation tests |
| R-O07 | Logs or metrics consume excessive storage | High | Medium | High | Define retention, rotation and aggregation policies |

---

## 6. Delivery Risks

| ID | Risk | Likelihood | Impact | Rating | Mitigation |
| --- | --- | --- | --- | --- | --- |
| R-D01 | Stories become too large | High | Medium | High | Apply story-size standards and split work before sprint entry |
| R-D02 | Dependencies are discovered too late | Medium | High | High | Use dependency fields and Definition of Ready checks |
| R-D03 | Documentation falls behind implementation | Medium | Medium | Medium | Include documentation in every Definition of Done |
| R-D04 | Too many features are attempted in one sprint | Medium | High | High | Protect sprint goals and move optional work to later sprints |
| R-D05 | External provider integration delays delivery | Medium | Medium | Medium | Isolate provider-specific work and support mock testing |
| R-D06 | Testing evidence is incomplete | Medium | Medium | Medium | Define evidence requirements in each story |
| R-D07 | Main branch becomes unstable | Low | High | Medium | Use feature branches, pull requests and mandatory build validation |

---

## 7. Product and Business Risks

| ID | Risk | Likelihood | Impact | Rating | Mitigation |
| --- | --- | --- | --- | --- | --- |
| R-B01 | Platform scope becomes unclear | Medium | High | High | Maintain product vision, requirements and exclusions |
| R-B02 | Version 2.0 duplicates existing tools without differentiation | Medium | Medium | Medium | Focus on integrated monitoring, edge operations and engineering visibility |
| R-B03 | User interface becomes too complex | Medium | Medium | Medium | Use role-aware navigation and progressive disclosure |
| R-B04 | Enterprise features are introduced too early | Medium | Medium | Medium | Complete core platform capabilities before advanced tenancy |
| R-B05 | Reports do not meet academic or professional needs | Low | Medium | Low | Review report templates against stakeholder requirements |

---

## 8. Highest-Priority Risks

The following risks require continuous attention:

- Breaking Version 1.0 compatibility
- Unsafe build execution
- Weak tenant isolation
- Unauthorised project access
- Uncontrolled monitoring-data growth
- Alert flooding
- Oversized Jira stories
- Unclear service ownership
- Database migration failure
- Secret exposure

These risks should be reviewed during architecture, sprint and release reviews.

---

## 9. Risk Ownership

Risk ownership should follow domain responsibility.

| Risk Area | Primary Owner |
| --- | --- |
| Architecture | Technical Lead |
| Security | Technical Lead and service owner |
| Database | Service owner |
| Frontend | Frontend owner |
| Edge Agent | Edge integration owner |
| DevOps and builds | DevOps capability owner |
| Jira scope | Product owner |
| Testing | Story owner |
| Documentation | Story owner |
| Release readiness | Project owner |

For the current project, overall risk ownership remains with Taha Aflouk.

---

## 10. Risk Review Process

Risks should be reviewed:

- Before each sprint
- During sprint planning
- When architecture changes
- Before external integrations
- Before database migrations
- Before deployment changes
- During sprint review
- Before release approval

New high-impact risks must be added immediately.

Resolved risks should remain recorded with their final outcome.

---

## 11. Risk Evidence

Risk controls should be supported by evidence such as:

- Security-test results
- Build logs
- Migration-test results
- Regression-test output
- Docker health output
- Raspberry Pi validation
- Monitoring screenshots
- Alert workflow evidence
- Pull-request reviews
- Architecture Decision Records

---

## 12. Escalation Rules

A risk must be escalated when:

- Its rating becomes High.
- A mitigation is no longer effective.
- It blocks a sprint goal.
- It may expose sensitive data.
- It threatens Version 1.0 compatibility.
- It could cause data loss.
- It creates an unsafe execution path.
- It affects release readiness.

A blocked story must not proceed until the risk is accepted or controlled.

---

## 13. Risk Acceptance

A risk may be accepted only when:

- The impact is understood.
- The reason is documented.
- The owner is identified.
- The remaining exposure is acceptable.
- A review date is defined.
- The acceptance does not violate security requirements.

High security risks should not normally be accepted without mitigation.

---

## 14. Current Status

**Status:** Draft

**Owner:** Taha Aflouk

**Version:** EdgeCloud Platform Version 2.0

**Previous document:** VERSION_2_ENGINEERING_STANDARDS.md

**Next document:** VERSION_2_DEPENDENCY_MATRIX.md
