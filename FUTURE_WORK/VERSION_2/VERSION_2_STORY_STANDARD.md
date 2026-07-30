# EdgeCloud Platform Version 2.0 Story Standard

## 1. Purpose

This document defines the required structure and quality standard for all EdgeCloud Platform Version 2.0 Jira stories.

The objective is to ensure that every story is:

- Clear
- Testable
- Traceable
- Secure
- Appropriately scoped
- Ready for implementation
- Supported by evidence
- Consistent across all sprints

---

## 2. Required Story Format

Every story should use the following structure.

### User Story

As a relevant platform user or stakeholder,  
I want a clearly defined capability,  
So that a measurable business or engineering benefit is achieved.

### Overview

The overview should explain:

- Why the story is required
- What problem it solves
- Which platform area it affects
- What is included
- What is excluded
- Any important technical context

---

## 3. Acceptance Criteria

Acceptance criteria must be:

- Specific
- Observable
- Testable
- Written from the user or system perspective
- Limited to the scope of the story

The preferred structure is:

### AC1 — Descriptive Title

Given a defined starting condition  
When a user or system action occurs  
Then a clear expected result must be produced

Each acceptance criterion should cover one primary behaviour.

Avoid acceptance criteria that:

- Combine unrelated behaviours
- Use vague wording
- Depend on undocumented assumptions
- Describe implementation details instead of outcomes
- Cannot be verified through testing

---

## 4. Story Scope

Every story must clearly identify:

### Included

- Functional behaviour
- API changes
- Database changes
- Frontend changes
- Security changes
- Tests
- Documentation

### Excluded

- Future enhancements
- Unrelated refactoring
- Additional providers
- Optional integrations
- Features planned for later sprints

This prevents scope expansion during implementation.

---

## 5. Jira Metadata

Every story should include:

- Epic
- Sprint
- Fix Version
- Priority
- Story Points
- Component
- Labels
- Assignee when known
- Requirement references
- Dependencies

Recommended labels include:

- backend
- frontend
- security
- database
- testing
- documentation
- monitoring
- edge
- alerting
- analytics
- devops
- enterprise

---

## 6. Requirement Traceability

Every story must reference one or more requirement identifiers from:

`VERSION_2_PRODUCT_REQUIREMENTS.md`

Example:

Related Requirements:

- FR-PROJ-001
- FR-PROJ-004
- SEC-002
- TEST-002
- DOC-001

The references must accurately match the story scope.

---

## 7. Dependencies

Every story must identify:

- Blocking stories
- Blocked stories
- Required services
- Required APIs
- Required data migrations
- Required infrastructure
- Required external integrations
- Security dependencies
- Documentation dependencies

A story should not begin while a critical dependency remains unresolved.

---

## 8. Technical Notes

Technical notes may include:

- Proposed service owner
- Expected API endpoint
- Expected entity or DTO changes
- Security requirements
- Migration considerations
- Integration points
- Logging requirements
- Performance considerations
- Backwards-compatibility concerns

Technical notes should guide implementation without unnecessarily restricting better solutions.

---

## 9. Security Requirements

Every story must consider:

- Authentication
- Authorisation
- Role enforcement
- Organisation scope
- Project scope
- Input validation
- Sensitive data
- Secret handling
- Audit logging
- Safe error handling
- Cross-tenant access
- Webhook verification where relevant

Security requirements must be enforced in backend services and not only in the frontend.

---

## 10. Testing Requirements

Every story must identify the required tests.

Possible test categories include:

- Unit tests
- Repository tests
- Service tests
- Controller tests
- Integration tests
- Security tests
- Frontend component tests
- End-to-end tests
- Regression tests
- Manual verification
- Raspberry Pi validation
- Docker Compose validation

Tests must directly verify the acceptance criteria.

---

## 11. Documentation Requirements

Every completed story must update relevant documentation.

Possible documentation updates include:

- API documentation
- Database documentation
- Architecture documentation
- Configuration documentation
- Deployment documentation
- User guidance
- Testing evidence
- Screenshots
- Sprint records
- Known limitations

Documentation should be completed as part of the story, not postponed indefinitely.

---

## 12. Evidence Requirements

Every story must produce suitable evidence.

Evidence may include:

- Passing test output
- Build output
- API responses
- Database records
- Screenshots
- Logs
- Docker health output
- Raspberry Pi output
- Security-test results
- Generated reports

Evidence should be stored in the appropriate project documentation location.

---

## 13. Definition of Ready

A story is ready for implementation when:

- The business value is clear.
- The user story is understandable.
- Acceptance criteria are testable.
- Scope is defined.
- Exclusions are clear.
- Dependencies are identified.
- Requirements are referenced.
- Security impact is considered.
- Data ownership is understood.
- Story points are assigned.
- The correct Epic and Sprint are selected.

---

## 14. Definition of Done

A story is complete when:

- All acceptance criteria are satisfied.
- Implementation follows engineering standards.
- Required tests pass.
- Security controls are implemented.
- Existing functionality remains operational.
- Database migrations are included where required.
- API documentation is updated.
- Relevant technical documentation is updated.
- Evidence is captured.
- Build validation passes.
- Docker Compose remains functional where relevant.
- Raspberry Pi compatibility is preserved where relevant.
- No critical defects remain.
- The pull request is reviewed and merged.

---

## 15. Story Size Standard

Stories should normally be small enough to complete within a sprint.

Guidance:

| Story Points | Interpretation |
| --- | --- |
| 1 | Very small change |
| 2 | Small and isolated |
| 3 | Standard story |
| 5 | Moderate cross-layer feature |
| 8 | Complex but manageable |
| 13 | Usually too large and should be split |

A story should be split when it contains:

- Multiple independent user outcomes
- Several unrelated APIs
- Major backend and frontend platforms
- Multiple database domains
- Unclear completion boundaries

---

## 16. Story Review Checklist

Before a story enters a sprint, confirm:

- The title is clear.
- The user story is meaningful.
- The overview explains the problem.
- Acceptance criteria are testable.
- Scope is controlled.
- Exclusions are listed.
- Dependencies are documented.
- Requirement references are correct.
- Security requirements are considered.
- Tests are identified.
- Documentation obligations are included.
- Evidence expectations are defined.
- Story points are appropriate.

---

## 17. Example Story Skeleton

### Title

Implement Project Registration

### User Story

As an authenticated platform user,  
I want to create a software project,  
So that services, repositories, devices and engineering data can be organised under one project.

### Overview

This story introduces the initial project-registration capability for Version 2.0.

### Acceptance Criteria

#### AC1 — Create Project

Given an authenticated authorised user  
When valid project details are submitted  
Then a new project must be created

#### AC2 — Validate Input

Given invalid or incomplete project details  
When the request is submitted  
Then the platform must return a clear validation response

#### AC3 — Protect Access

Given an unauthorised user  
When project creation is attempted  
Then access must be denied

### Related Requirements

- FR-PROJ-001
- FR-PROJ-002
- SEC-001
- SEC-002
- TEST-002

### Definition of Done

- Project creation is implemented.
- Validation is implemented.
- Authorisation is enforced.
- Tests pass.
- API documentation is updated.
- Evidence is captured.

---

## 18. Current Status

**Status:** Draft

**Owner:** Taha Aflouk

**Version:** EdgeCloud Platform Version 2.0

**Previous document:** VERSION_2_JIRA_ROADMAP.md

**Next document:** VERSION_2_ENGINEERING_STANDARDS.md
