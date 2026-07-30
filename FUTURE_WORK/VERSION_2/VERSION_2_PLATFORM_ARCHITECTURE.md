# EdgeCloud Platform Version 2.0 Platform Architecture

## 1. Document Purpose

This document defines the proposed platform architecture for EdgeCloud Platform Version 2.0.

It describes:

- The existing Version 1.0 architecture
- The target Version 2.0 architecture
- Service responsibilities
- Domain boundaries
- Integration patterns
- Data ownership
- Security boundaries
- Deployment direction
- Migration principles
- Architecture risks
- Future scalability considerations

This document provides the technical foundation for the Version 2.0 Jira roadmap and implementation stories.

---

## 2. Architecture Objectives

The Version 2.0 architecture must:

1. Preserve the working Version 1.0 platform.
2. Support both microservice and Raspberry Pi monitoring.
3. Introduce project-oriented organisation.
4. Connect repositories, builds, tests, deployments and runtime monitoring.
5. Maintain clear service and database ownership.
6. Support secure GitHub integration.
7. Introduce CI/CD and code-quality foundations incrementally.
8. Support intelligent alerting and incident management.
9. Provide engineering analytics and professional reporting.
10. Establish multi-tenant and SaaS-ready foundations.
11. Remain deployable through Docker Compose.
12. Avoid unnecessary microservice complexity.

---

## 3. Version 1.0 Architecture Baseline

EdgeCloud Monitor Version 1.0 currently contains the following main components:

### 3.1 Discovery Service

The Discovery Service uses Netflix Eureka to provide:

- Service registration
- Service discovery
- Dynamic service location
- Microservice availability visibility

### 3.2 API Gateway

The API Gateway provides:

- Central API routing
- External entry-point control
- Authentication-token forwarding
- Route organisation
- Cross-origin configuration
- Separation between clients and internal services

### 3.3 Authentication Service

The Authentication Service provides:

- User registration
- User authentication
- Password protection
- JWT generation
- JWT validation support
- Role-based access control

### 3.4 Monitoring Service

The Monitoring Service provides:

- Telemetry ingestion
- CPU metric storage
- Memory metric storage
- Temperature metric storage
- Historical metric retrieval
- Monitoring-data access for the dashboard

### 3.5 Device Service

The Device Service provides:

- Edge-device registration
- Device metadata
- Heartbeat processing
- Online and offline status
- Device history
- Raspberry Pi device management

### 3.6 Alert Service

The Alert Service provides:

- Threshold evaluation
- Alert creation
- Alert storage
- Alert retrieval
- Alert status workflows
- Alert presentation through the dashboard

### 3.7 React Dashboard

The React dashboard provides:

- User authentication
- Device visibility
- Telemetry visualisation
- Historical charts
- Alert visibility
- Operational summaries
- User-facing platform navigation

### 3.8 Raspberry Pi Edge Agent

The Python-based edge agent provides:

- CPU telemetry collection
- Memory telemetry collection
- Temperature telemetry collection
- Heartbeat transmission
- REST communication with backend services
- Raspberry Pi compatibility
- Simulated telemetry support

### 3.9 Docker Compose Environment

Docker Compose currently coordinates:

- Backend microservices
- Service discovery
- API Gateway
- Databases
- Inter-service networking
- Environment-based configuration
- Local deployment and validation

---

## 4. Version 1.0 Architectural Strengths

The Version 1.0 architecture already provides strong foundations:

- Independently deployable Spring Boot services
- Clear initial monitoring domains
- API-driven communication
- Service discovery
- Gateway-based routing
- JWT security
- Role-based access
- Dedicated Raspberry Pi integration
- Historical monitoring data
- Docker-based deployment
- A working React frontend
- Demonstrated end-to-end operation

Version 2.0 should extend these strengths rather than replace them without clear justification.

---

## 5. Version 1.0 Architectural Limitations

Version 1.0 does not yet provide a complete engineering operations model.

Current limitations include:

- No central software-project domain
- No repository-registration workflow
- No GitHub integration
- No webhook-processing architecture
- No native build records
- No test-result domain
- No code-quality domain
- No quality-gate domain
- No deployment-history domain
- Limited microservice observability
- Limited container visibility
- Limited alert acknowledgement and escalation
- No incident-management domain
- No organisation or tenant model
- No engineering analytics layer
- No professional report-generation domain

Version 2.0 must address these limitations incrementally.

---

## 6. Target Architecture Style

Version 2.0 will continue using a cloud-native microservice architecture.

However, the platform must avoid creating a new microservice for every database table or small feature.

A new service should only be introduced when at least one of the following applies:

- The domain has a clear independent responsibility.
- The domain requires independent scaling.
- The domain has distinct security boundaries.
- The domain has distinct availability requirements.
- The domain owns high-volume data.
- The domain performs isolated background processing.
- The domain has a clear independent lifecycle.
- Adding the capability to an existing service would create poor cohesion.

Small related capabilities should remain grouped within a coherent service.

---

## 7. Core Architecture Principles

### 7.1 Database Ownership

Each microservice owns its database.

A service must not directly read or modify another service’s database.

### 7.2 API-Driven Communication

Cross-service communication must use documented APIs or approved asynchronous events.

### 7.3 Logical Cross-Service References

Cross-service relationships must use logical identifiers rather than foreign keys across service databases.

### 7.4 Stateless Application Services

Application services should remain stateless where practical to support replacement and horizontal scaling.

### 7.5 Secure Defaults

New integrations and externally reachable endpoints must remain disabled or protected until configured securely.

### 7.6 Incremental Migration

Version 2.0 capabilities must be introduced without requiring a complete rewrite of Version 1.0.

### 7.7 Backwards Compatibility

Existing device, telemetry, heartbeat, alert and dashboard workflows must remain operational during staged development.

### 7.8 Observable Platform Services

Every new service must expose health information and appropriate structured logs.

### 7.9 Explicit Domain Boundaries

Every new entity, API and workflow must have a clearly identified owning service.

### 7.10 Evidence-Based Architecture

Architecture decisions must be supported by documented requirements, risks and operational evidence.


---

## 8. Target Platform Domain Model

Version 2.0 will organise platform data around a central software-project model.

The high-level relationship is:

```text
Organisation
    ↓
Project
    ↓
Repository
    ↓
Build
    ↓
Test and Quality Results
    ↓
Deployment
    ↓
Runtime Services and Edge Devices
    ↓
Metrics
    ↓
Alerts
    ↓
Incidents
    ↓
Analytics and Reports
The project becomes the primary business and engineering context for Version 2.0.
A project may contain:
One or more repositories
One or more microservices
One or more edge devices
Build history
Test results
Code-quality results
Quality-gate results
Deployment history
Runtime metrics
Alerts
Incidents
Reports
Members and permissions
9. Proposed Version 2.0 Service Landscape
The following architecture is the initial target direction.
It distinguishes between:
Existing services that should be preserved
Existing services that may be extended
New services that may be introduced after architecture review
Capabilities that should remain modules until extraction is justified
10. Existing Services to Preserve
10.1 Discovery Service
The Discovery Service remains responsible for:
Eureka service registration
Dynamic service discovery
Service availability visibility
It should not own:
Project records
Monitoring history
Build records
Alert rules
Organisation data
10.2 API Gateway
The API Gateway remains responsible for:
External API entry
Route management
Authentication integration
Cross-origin handling
Request forwarding
Future rate-limiting enforcement
Future correlation identifiers
It should not contain domain business logic.
10.3 Authentication Service
The Authentication Service remains responsible for:
Authentication
Credential protection
Token creation
Token validation support
User identity
Platform-level roles
It may later be extended to support:
Organisation membership
User status
Invitations
Role assignments
Session security
Token revocation
Account suspension
The exact ownership of organisation membership must be confirmed during enterprise architecture planning.
10.4 Monitoring Service
The Monitoring Service remains responsible for:
Telemetry ingestion
Runtime metrics
Historical metrics
Service metrics
Edge metrics
Metric aggregation
Metric retrieval
Monitoring health summaries
It may be extended to support:
JVM metrics
API response times
Error rates
Container metrics
Service availability history
Project-aware metrics
Aggregated time-series views
The Monitoring Service should not own:
Repository credentials
Build workflows
Quality findings
Deployment approvals
User permissions
10.5 Device Service
The Device Service remains responsible for:
Device registration
Device identity
Device metadata
Heartbeats
Online and offline state
Device availability history
Device groups
Agent version
Project association for devices
It should not own raw long-term telemetry if the Monitoring Service remains the metric owner.
10.6 Alert Service
The Alert Service remains responsible for:
Alert rules
Threshold evaluation
Alert creation
Alert status
Alert acknowledgement
Alert resolution
Alert deduplication
Escalation
Notification coordination
Alert history
It may consume events or API data from:
Monitoring Service
Build capability
Quality capability
Deployment capability
Device Service
11. Proposed New Platform Capabilities
The following capabilities are required by Version 2.0.
They do not all need to become independent microservices immediately.
11.1 Project Management Capability
The Project Management capability should own:
Projects
Project metadata
Project status
Project tags
Project membership
Project roles
Project archiving
Project health references
Initial architectural recommendation:
Create a dedicated Project Service because the project becomes the primary organisational boundary for Version 2.0.
Proposed service name:
edgecloud-project-service
11.2 Repository Integration Capability
The Repository Integration capability should own:
Registered repositories
Provider configuration
GitHub integration state
Webhook configuration
Webhook event history
Commit metadata
Synchronisation status
Initial architectural recommendation:
Start as a dedicated integration module or service depending on implementation scope.
Preferred future service name:
edgecloud-integration-service
This service should isolate provider-specific behaviour from core project logic.
11.3 Build and Automation Capability
The Build capability should own:
Build definitions
Build records
Build status
Build triggers
Build logs
Build timeouts
Build cancellation
Build artefact metadata
Build execution must be isolated from the main platform services.
Initial recommendation:
Separate the control plane from the execution plane.
Build Control Plane
    ↓
Build Job Queue
    ↓
Isolated Build Runner
    ↓
Build Results
The build-control capability may initially be implemented within a DevOps service.
The build runner should remain a separate process or container.
11.4 Test Result Capability
The Test Result capability should own:
Test-suite summaries
Individual test failures where appropriate
Test duration
Test framework
Imported test reports
Build association
Historical test trends
This capability may initially remain within the DevOps or Quality service.
11.5 Code Quality Capability
The Code Quality capability should own:
Static-analysis results
Coverage results
Complexity results
Duplication indicators
Quality findings
Finding severity
Finding lifecycle
Quality history
Quality-gate rules
Quality-gate evaluations
Initial architectural recommendation:
Create a Quality Service once the domain requires independent analysis and persistence.
Proposed service name:
edgecloud-quality-service
11.6 Deployment Capability
The Deployment capability should own:
Deployment records
Environments
Deployment status
Approval records
Deployment evidence
Rollback evidence
Build and commit traceability
Initial architectural recommendation:
Begin as a module within a DevOps service.
Extract a dedicated Deployment Service only if deployment execution, approvals or scaling justify separation.
11.7 Incident Management Capability
The Incident capability should own:
Incidents
Severity
Status
Ownership
Timelines
Related alerts
Investigation notes
Root-cause notes
Resolution summaries
Initial recommendation:
The incident domain may begin within the Alert Service because alerts and incidents are closely related.
It should be extracted later only if the domain becomes independently complex.
11.8 Analytics Capability
The Analytics capability should provide:
Project-health calculation
Trend aggregation
Reliability indicators
DORA-inspired metrics
Business summaries
Engineering summaries
Cross-domain read models
Analytics should not directly query every service database.
It should consume:
Service APIs
Approved events
Replicated read models
Aggregated datasets
Initial recommendation:
Create an Analytics Service when cross-domain reporting becomes substantial.
Proposed service name:
edgecloud-analytics-service
11.9 Reporting Capability
The Reporting capability should provide:
Report definitions
Report generation
PDF export
CSV export
Evidence packaging
Report metadata
Report history
It may initially be part of the Analytics Service.
A separate Reporting Service is not required unless report generation becomes resource-intensive or independently scalable.
11.10 Organisation and Tenant Capability
The Enterprise capability should own or coordinate:
Organisations
Organisation memberships
Teams
Organisation roles
Tenant configuration
Audit context
Tenant-aware permissions
The final ownership decision must consider the current Authentication Service.
Possible options include:
Extend the Authentication Service.
Introduce an Organisation Service.
Use a shared identity boundary with separate organisation ownership.
The chosen design must avoid duplicated user identity records.
12. Initial Recommended Service Set
The initial recommended Version 2.0 service set is:
Existing services
Discovery Service
API Gateway
Authentication Service
Monitoring Service
Device Service
Alert Service
Recommended new services
Project Service
Integration Service
Quality Service
Analytics Service
Capabilities that may initially remain grouped
Build control
Test results
Deployment records
Reporting
Incident management
Organisation management
This approach avoids introducing too many services before the domain boundaries are proven.
13. Service Ownership Matrix
Domain	Initial Owner
Authentication	Authentication Service
User identity	Authentication Service
Platform roles	Authentication Service
Projects	Project Service
Project membership	Project Service
Repository metadata	Integration Service
GitHub integration	Integration Service
Webhooks	Integration Service
Build records	DevOps capability
Build execution	Isolated Build Runner
Test results	DevOps or Quality capability
Quality findings	Quality Service
Quality gates	Quality Service
Deployment records	DevOps capability
Runtime metrics	Monitoring Service
Historical telemetry	Monitoring Service
Device identity	Device Service
Device heartbeats	Device Service
Alert rules	Alert Service
Alerts	Alert Service
Incidents	Alert Service initially
Analytics	Analytics Service
Reports	Analytics Service initially
Organisations	To be confirmed
Audit records	Domain-owned events plus central read model

14. Cross-Service Reference Rules
Cross-service references should use stable logical identifiers.
Examples include:
organisationId
projectId
repositoryId
buildId
deploymentId
serviceId
deviceId
alertId
incidentId
userId
A service may store another service’s identifier for correlation.
It must not enforce a database foreign key into another service’s database.
Validation may be performed using:
Synchronous API calls
Cached reference data
Asynchronous events
Deferred validation where appropriate

---

## 15. Communication Strategy

Version 2.0 will use two communication styles.

### Synchronous communication

REST APIs should be used when:

- An immediate response is required
- A user-facing operation depends on validation
- Data must be retrieved directly
- The workflow is short and predictable

### Asynchronous communication

Events should be considered when:

- Build results are completed
- Deployments change status
- Quality gates are evaluated
- Alerts are created
- Incidents are updated
- Metrics require background aggregation

Asynchronous communication must include:

- Stable event identifiers
- Event timestamps
- Source service
- Resource identifiers
- Retry handling
- Idempotent consumers
- Failure visibility

---

## 16. Security Architecture

The security architecture must enforce:

- Authentication at protected entry points
- Backend authorisation
- Organisation and project scope
- Least-privilege access
- Secure token handling
- Webhook signature verification
- Secret protection
- Audit logging
- Input validation
- Safe error responses

Build execution must remain isolated from the main application runtime.

Untrusted repository code must not execute inside:

- API Gateway
- Authentication Service
- Project Service
- Monitoring Service
- Device Service
- Alert Service
- Quality Service
- Analytics Service

---

## 17. Data Architecture

Each service must own its persistence model.

Recommended data categories include:

- Relational data for projects, users, builds, alerts and configuration
- Time-series-style data for metrics and telemetry
- Object or file storage for reports, logs and artefact metadata
- Audit records for sensitive operations

High-volume data must use:

- Retention policies
- Pagination
- Aggregation
- Suitable indexes
- Controlled export
- Archiving where appropriate

---

## 18. Deployment Architecture

Docker Compose remains the reference environment for Version 2.0 development and demonstration.

The target deployment should include:

- Service discovery
- API Gateway
- Existing platform services
- Approved new services
- Service-owned databases
- Health checks
- Environment-based configuration
- Internal Docker networks
- Persistent volumes where required

The architecture should remain compatible with future container orchestration, but Kubernetes is not required for the initial Version 2.0 release.

---

## 19. Migration Strategy

Version 2.0 will use incremental migration.

The migration sequence should be:

1. Preserve Version 1.0 services and APIs.
2. Introduce the Project Service.
3. Associate existing services and devices with projects.
4. Extend observability.
5. Improve alerting.
6. Extend edge-device management.
7. Introduce analytics and reporting.
8. Introduce repository and quality integrations.
9. Introduce organisation and tenant foundations.

Every migration affecting existing data must include:

- Compatibility assessment
- Migration script
- Backup plan
- Regression testing
- Rollback procedure
- Updated documentation

---

## 20. Architecture Risks

Key architecture risks include:

- Excessive microservice fragmentation
- Tight coupling through synchronous APIs
- Duplicate identity or organisation data
- Uncontrolled metric growth
- Unsafe build execution
- Weak tenant isolation
- Webhook spoofing
- Alert flooding
- Cross-domain reporting complexity
- Breaking Version 1.0 workflows

These risks will be expanded in `VERSION_2_RISK_ASSESSMENT.md`.

---

## 21. Architecture Decision Requirements

Significant technical decisions must document:

- Context
- Decision
- Alternatives considered
- Benefits
- Risks
- Security impact
- Data impact
- Operational impact
- Migration impact

Architecture decisions should be stored as Architecture Decision Records when implementation begins.

---

## 22. Architecture Readiness Criteria

The architecture is ready to support Jira planning when:

- Existing services and responsibilities are documented.
- Proposed service boundaries are understood.
- The Project Service is accepted as the Version 2.0 foundation.
- Data ownership is clear.
- Cross-service references use logical identifiers.
- Build execution isolation is mandatory.
- Security boundaries are documented.
- Version 1.0 compatibility is protected.
- Docker Compose remains supported.
- Migration will occur incrementally.

---

## 23. Current Status

**Status:** Draft

**Owner:** Taha Aflouk

**Version:** EdgeCloud Platform Version 2.0

**Previous document:** VERSION_2_PRODUCT_REQUIREMENTS.md

**Next document:** VERSION_2_JIRA_ROADMAP.md
