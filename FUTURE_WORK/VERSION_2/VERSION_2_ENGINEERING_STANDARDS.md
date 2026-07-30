# EdgeCloud Platform Version 2.0 Engineering Standards

## 1. Purpose

This document defines the engineering standards for EdgeCloud Platform Version 2.0.

These standards apply to:

- Backend services
- Frontend applications
- Edge agents
- Databases
- APIs
- Security
- Testing
- Documentation
- Docker deployment
- Git workflow

---

## 2. Core Engineering Principles

All Version 2.0 work must follow these principles:

- Inspect before coding
- Reuse existing services
- Preserve Version 1.0 behaviour
- Keep changes small and reviewable
- Build after every logical change
- Test before merge
- Avoid unnecessary refactoring
- Prefer secure defaults
- Document important decisions
- Keep main branch stable

---

## 3. Backend Standards

Backend services should use:

- Spring Boot
- Constructor injection
- Clear package boundaries
- DTOs for API communication
- Service-layer business logic
- Repository abstraction
- Central exception handling
- Bean validation
- Structured logging
- Environment-based configuration

Controllers should not contain complex business logic.

Entities should not be exposed directly through public APIs.

---

## 4. Microservice Standards

Each microservice must have:

- A clear domain responsibility
- Its own database
- Independent configuration
- Health endpoints
- Structured logs
- API documentation
- Automated tests
- Docker support
- Error handling
- Security rules

A service must not access another service’s database directly.

Cross-service references must use logical identifiers.

---

## 5. API Standards

APIs should use:

- Versioned paths
- Consistent resource naming
- Standard HTTP methods
- Appropriate status codes
- Request validation
- Predictable error responses
- Pagination for large collections
- Filtering where useful
- Authentication and authorisation
- OpenAPI documentation

Example path style:

`/api/v2/projects`

Sensitive internal details must not be exposed in error responses.

---

## 6. Database Standards

Database changes must include:

- Clear table ownership
- Migration scripts
- Appropriate indexes
- Validation constraints
- Audit timestamps where needed
- Backwards-compatibility review
- Rollback consideration

Cross-service foreign keys are prohibited.

High-volume tables must support retention and pagination.

---

## 7. Security Standards

Security must be enforced in backend services.

Required controls include:

- Authentication
- Role-based authorisation
- Project and organisation scope
- Input validation
- Password protection
- Secret protection
- Webhook signature validation
- Least privilege
- Safe error handling
- Audit logging

Frontend role checks improve user experience but do not replace backend enforcement.

---

## 8. Build Execution Standards

Untrusted repository code must run only in isolated build environments.

Build runners must have:

- Resource limits
- Timeouts
- Restricted network access
- Temporary workspaces
- Controlled environment variables
- Safe log handling
- Cleanup after execution

Build execution must never occur inside core platform services.

---

## 9. Frontend Standards

The React application should use:

- Reusable components
- Clear page structure
- Central API services
- Consistent loading states
- Consistent error states
- Responsive layouts
- Accessible controls
- Role-aware navigation
- Secure token handling
- Professional visual consistency

Business logic should not be duplicated across components.

---

## 10. Edge Agent Standards

The Raspberry Pi agent should use:

- Environment-based configuration
- Clear telemetry loops
- Retry handling
- Timeout handling
- Structured logs
- Graceful shutdown
- Version reporting
- Backwards-compatible payloads
- Lightweight dependencies
- Raspberry Pi validation

The agent must continue supporting simulated telemetry where required.

---

## 11. Testing Standards

Required tests should be selected based on story scope.

Test types may include:

- Unit tests
- Repository tests
- Service tests
- Controller tests
- Integration tests
- Security tests
- Frontend tests
- End-to-end tests
- Docker validation
- Raspberry Pi validation
- Regression tests

Every acceptance criterion must have direct test evidence.

---

## 12. Logging Standards

Logs should include:

- Timestamp
- Service name
- Log level
- Correlation identifier where available
- Relevant resource identifier
- Clear message
- Error context

Logs must not expose:

- Passwords
- Tokens
- Secrets
- Sensitive personal data
- Full credentials

---

## 13. Configuration Standards

Configuration must use environment variables or approved external configuration.

Do not hard-code:

- Passwords
- Tokens
- Database credentials
- Provider secrets
- Webhook secrets
- Production URLs

Development defaults must be clearly documented.

---

## 14. Docker Standards

Docker images should:

- Use suitable base images
- Minimise unnecessary packages
- Expose only required ports
- Use environment configuration
- Support health checks
- Avoid storing secrets
- Use reproducible builds

Docker Compose must remain usable for local development and demonstration.

---

## 15. Git Workflow

Recommended workflow:

1. Update main
2. Create a story branch
3. Implement one scoped story
4. Run tests
5. Run builds
6. Review changed files
7. Commit with a clear message
8. Push the branch
9. Create a pull request
10. Review and merge
11. Confirm main remains stable

Recommended branch naming:

`feature/SCRUM-XXX-short-description`

`fix/SCRUM-XXX-short-description`

`docs/SCRUM-XXX-short-description`

---

## 16. Commit Standards

Commits should be:

- Small
- Focused
- Descriptive
- Related to one logical change

Example:

`feat(projects): add project registration endpoint`

Avoid vague messages such as:

- update
- changes
- fix stuff
- final
- test

---

## 17. Pull Request Standards

Every pull request should include:

- Story reference
- Summary
- Main changes
- Testing performed
- Screenshots where relevant
- Security considerations
- Database changes
- Known limitations
- Documentation updates

A pull request should not contain unrelated work.

---

## 18. Documentation Standards

Documentation should use:

- British English
- Clear headings
- Consistent terminology
- Current file paths
- Accurate commands
- Professional screenshots
- Traceable evidence

Documentation must be updated with the implementation.

---

## 19. Quality Gates

Before merge, verify:

- Backend builds pass
- Frontend builds pass
- Tests pass
- Security checks pass
- Docker configuration remains valid
- API documentation is updated
- Database migrations are included
- No secrets are committed
- Existing workflows remain functional

---

## 20. Definition of Engineering Readiness

A change is engineering-ready when:

- Scope is understood
- Ownership is clear
- Dependencies are resolved
- Security impact is reviewed
- Data impact is reviewed
- Tests are planned
- Documentation impact is known
- Rollback is considered

---

## 21. Current Status

**Status:** Draft

**Owner:** Taha Aflouk

**Version:** EdgeCloud Platform Version 2.0

**Previous document:** VERSION_2_STORY_STANDARD.md

**Next document:** VERSION_2_RISK_ASSESSMENT.md
