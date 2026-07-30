# EdgeCloud Platform Version 2.0 Product Vision

## 1. Document Purpose

This document defines the product vision for EdgeCloud Platform Version 2.0.

It establishes the strategic direction, intended users, business value, product boundaries and long-term evolution of the platform before detailed requirements, architecture and Jira stories are created.

This document acts as a decision-making reference for all Version 2.0 planning and implementation work.

---

## 2. Version 1.0 Baseline

EdgeCloud Monitor Version 1.0 was created as a cloud-native monitoring platform for edge devices and distributed services.

The completed baseline includes:

- Spring Boot microservices
- Netflix Eureka service discovery
- API Gateway routing
- JWT authentication and role-based access control
- Monitoring Service
- Device Service
- Alert Service
- React dashboard
- Raspberry Pi edge telemetry agent
- Device heartbeat processing
- CPU, memory and temperature telemetry
- Historical metric storage
- Threshold-based alerts
- Docker Compose deployment
- Testing and deployment evidence
- Technical and academic documentation

The existing Raspberry Pi workflow is operational and must remain fully supported.

Version 2.0 must extend the platform without weakening or unnecessarily rebuilding the working Version 1.0 foundation.

---

## 3. Product Evolution

Version 1.0 focused primarily on monitoring edge devices.

Version 2.0 will evolve the product into a broader Engineering Operations Platform capable of monitoring and supporting the complete lifecycle of modern software systems.

The platform will connect operational information that is commonly separated across multiple tools, including:

- Application and microservice monitoring
- Edge-device monitoring
- Repository and project management
- Build execution
- Automated testing
- Static code analysis
- Quality gates
- Deployment tracking
- Alerting
- Incident management
- Engineering analytics
- Business reporting

The platform will provide a unified view of software quality, delivery health and runtime performance.

---

## 4. Vision Statement

EdgeCloud Platform will provide developers, engineering teams, technical managers, students and organisations with a unified environment for building, validating, deploying, monitoring and improving distributed software systems.

The platform will reduce the need to operate disconnected tools by combining practical observability, CI/CD, code-quality, alerting, analytics and edge-management capabilities in one accessible system.

---

## 5. Mission Statement

The mission of EdgeCloud Platform is to make professional software engineering operations more accessible, understandable and manageable for small teams, start-ups, educational environments and organisations operating cloud-native or edge-based systems.

The platform will prioritise:

- Clear operational visibility
- Practical automation
- Secure engineering workflows
- Actionable quality information
- Simple deployment and configuration
- Educational value
- Professional reporting
- Incremental adoption

---

## 6. Product Problem

Software teams frequently depend on multiple disconnected tools to understand their systems.

A typical workflow may require:

- GitHub for source control
- Jenkins for automation
- SonarQube for code quality
- JaCoCo for coverage
- Postman for API validation
- Docker for deployment
- Grafana or another dashboard for monitoring
- Email or messaging tools for alerts
- Manual reports for management

This creates several problems:

- Information is fragmented.
- Teams must maintain many tools.
- Students struggle to understand how the tools connect.
- Small organisations may lack the resources to configure enterprise platforms.
- Runtime failures may not be linked to source-code quality or deployment history.
- Managers may receive technical information without clear business context.
- Edge devices and microservices are often monitored separately.
- Root-cause investigation becomes slower.

EdgeCloud Platform Version 2.0 will address these problems by providing a single operational model connecting projects, repositories, services, devices, builds, deployments, quality results, metrics, alerts and incidents.

---

## 7. Product Positioning

EdgeCloud Platform Version 2.0 is positioned as a unified Engineering Operations Platform.

It is not intended to immediately replace every advanced capability of established enterprise products.

Instead, it will provide a focused and integrated alternative for users who need:

- Microservice observability
- Raspberry Pi and edge-device monitoring
- Build and test automation
- Code-quality analysis
- Quality-gate enforcement
- Deployment visibility
- Intelligent alerting
- Operational analytics
- Educational transparency
- Simplified platform management

The platform should be particularly valuable where Jenkins, SonarQube, monitoring tools and reporting systems would otherwise need to be configured and maintained separately.

---

## 8. Target Users

### 8.1 Software Developers

Developers require visibility into:

- Build results
- Test failures
- Code quality
- Test coverage
- Service health
- Runtime errors
- Deployment history
- Alerts linked to their projects

### 8.2 DevOps and Platform Engineers

DevOps and platform engineers require:

- Service discovery
- Microservice health monitoring
- Container visibility
- Deployment tracking
- Alert configuration
- Operational history
- Automation workflows
- Incident support
- Infrastructure evidence

### 8.3 Technical Managers

Technical managers require:

- Project health summaries
- Quality-gate results
- Delivery trends
- Deployment frequency
- Failure rates
- Incident summaries
- Team-level reports
- Risk visibility

### 8.4 Business Stakeholders

Business users require clear, non-technical views of:

- Platform availability
- Service health
- Operational risks
- Recent incidents
- Delivery confidence
- Project progress
- Business impact

### 8.5 Students and Educators

Students and educators require:

- Transparent CI/CD workflows
- Understandable quality reports
- Clear monitoring data
- Traceable project evidence
- Practical DevOps examples
- Accessible architecture
- Reproducible learning environments

### 8.6 Edge and IoT Teams

Edge and IoT teams require:

- Raspberry Pi monitoring
- Device registration
- Heartbeats
- Telemetry
- Device availability
- Historical metrics
- Fleet visibility
- Edge alerting

---

## 9. Core Product Capabilities

Version 2.0 will progressively introduce the following capability areas.

### 9.1 Project Management Foundation

The platform must allow users to register software projects and associate them with:

- Repositories
- Microservices
- Containers
- Edge devices
- Builds
- Deployments
- Metrics
- Alerts
- Incidents
- Reports

This project model will become the central organisational structure of Version 2.0.

### 9.2 Advanced Observability

The platform will monitor:

- Spring Boot microservices
- JVM metrics
- Service health
- API availability
- Docker containers
- Dependency relationships
- Historical runtime metrics
- Raspberry Pi devices
- Edge telemetry

### 9.3 Intelligent Alerting

The platform will support:

- Configurable alert rules
- Severity levels
- Alert deduplication
- Alert acknowledgement
- Escalation
- Notification channels
- Alert history
- Project-aware alerts

### 9.4 Edge Device Management

The platform will extend the working Version 1.0 edge functionality with:

- Fleet views
- Device grouping
- Device status history
- Enhanced heartbeat monitoring
- Device metadata
- Remote configuration planning
- Improved edge analytics

### 9.5 Analytics and Reporting

The platform will provide:

- Engineering dashboards
- Operational trends
- Project health scores
- Reliability indicators
- Build trends
- Deployment trends
- Quality trends
- Management reports
- Student evidence reports
- Exportable reports

### 9.6 DevOps and Quality Automation

The platform will progressively provide capabilities that reduce dependence on separate Jenkins and SonarQube installations.

These capabilities may include:

- Repository registration
- GitHub integration
- Webhook processing
- Build triggering
- Build status tracking
- Test execution
- Test-result collection
- JaCoCo coverage ingestion
- Static analysis
- Complexity analysis
- Technical-debt indicators
- Quality gates
- Deployment workflows
- Deployment history
- Rollback evidence

### 9.7 Enterprise and SaaS Readiness

The platform will introduce foundations for:

- Organisations
- Teams
- Projects
- Role-based permissions
- Tenant isolation
- Audit history
- Subscription planning
- Platform administration
- Secure secret handling
- Configurable retention

---

## 10. Raspberry Pi Continuity

Raspberry Pi support remains a first-class feature.

The existing edge agent and telemetry workflow must not be treated as obsolete or replaced without justification.

Version 2.0 must preserve:

- Device registration
- Heartbeat transmission
- CPU telemetry
- Memory telemetry
- Temperature telemetry
- Historical metric retrieval
- Threshold-based alerting
- Dashboard visibility
- Docker-based backend compatibility

Future edge stories should extend this foundation rather than recreate it.

Potential extensions include:

- Fleet management
- Device groups
- Improved offline detection
- Device health scoring
- Remote configuration
- Deployment of edge workloads
- Edge software version tracking
- Edge security status
- Device-level incident correlation

---

## 11. Relationship to Jenkins and SonarQube

Version 2.0 aims to reduce the need for separate Jenkins and SonarQube installations by introducing native automation and code-quality capabilities.

This does not mean every enterprise feature will be recreated immediately.

The replacement strategy must be incremental.

### Phase 1

- Repository registration
- GitHub integration
- Webhooks
- Build records
- Test-result ingestion
- Coverage reporting
- Basic quality rules
- Quality-gate status

### Phase 2

- Build execution
- Configurable pipeline stages
- Static analysis
- Complexity indicators
- Deployment automation
- Failure notifications

### Phase 3

- Pipeline templates
- Parallel tasks
- Environment promotion
- Approval gates
- Advanced quality rules
- Policy enforcement
- Historical comparison

Every implemented capability must be clearly distinguished from future planned functionality.

---

## 12. Product Principles

Version 2.0 must follow these principles.

### 12.1 Preserve Working Features

Existing Version 1.0 functionality must remain stable.

### 12.2 Integrate Before Rebuilding

The platform should initially integrate with existing tools and formats where appropriate before attempting full replacement.

### 12.3 Reuse Before Extraction

Existing microservices should be extended where domain ownership remains clear.

A new microservice should only be created when it provides a justified architectural boundary.

### 12.4 Secure by Default

Authentication, authorisation, tenant isolation, webhook validation and secret management must be designed before broad exposure.

### 12.5 Evidence-Based Operations

Alerts, quality results and recommendations must be supported by measurable evidence.

### 12.6 Explainability

The platform must explain why a build failed, why a quality gate failed or why an alert was raised.

### 12.7 Professional Simplicity

Complex engineering information should be presented through clear dashboards and workflows.

### 12.8 Incremental Delivery

Each sprint must provide demonstrable value without depending on unfinished future capability.

### 12.9 Educational Transparency

Where possible, the platform should help students understand the relationship between code, builds, deployments and runtime behaviour.

### 12.10 Business Relevance

Technical metrics should be translated into meaningful project and operational indicators for managers and business users.

---

## 13. Business Objectives

Version 2.0 aims to:

- Broaden the platform beyond edge-device monitoring.
- Support monitoring of real microservice systems.
- Reduce dependence on disconnected engineering tools.
- Improve developer visibility.
- Improve release confidence.
- Improve software-quality awareness.
- Improve incident response.
- Support technical and non-technical reporting.
- Create a stronger portfolio and commercial product.
- Establish foundations for future SaaS deployment.
- Preserve and strengthen Raspberry Pi support.
- Provide educational value for cloud-native and DevOps learning.

---

## 14. Success Measures

Version 2.0 will be considered successful when users can:

- Register a software project.
- Associate repositories, microservices and edge devices with that project.
- View project-level health.
- Monitor microservice and JVM performance.
- Continue monitoring Raspberry Pi devices.
- View build and test history.
- View code-quality and coverage results.
- Evaluate a quality gate.
- Track deployments.
- Configure and acknowledge alerts.
- Review incidents and operational history.
- Access engineering and business dashboards.
- Generate professional reports.
- Manage users, organisations and permissions securely.

---

## 15. Version 2.0 Scope

Version 2.0 includes:

- Project registration
- Microservice monitoring
- Advanced metrics
- Intelligent alerting
- Raspberry Pi fleet improvements
- Engineering analytics
- Reporting
- Repository integration
- CI/CD foundations
- Code-quality analysis
- Quality gates
- Deployment tracking
- Organisation and user governance
- SaaS-readiness foundations

---

## 16. Out of Scope for Initial Version 2.0 Delivery

The following are not immediate commitments unless approved through later planning:

- Full replacement of every Jenkins plugin
- Full replacement of every SonarQube analyser
- Kubernetes cluster management
- Multi-cloud infrastructure provisioning
- Automatic production remediation without approval
- Fully autonomous AI operations
- Enterprise billing
- Global high-availability deployment
- Support for every programming language
- Support for every source-control provider
- Native mobile applications
- Complex marketplace functionality

These may become future roadmap opportunities.

---

## 17. Competitive Differentiation

EdgeCloud Platform will differentiate itself through the combination of:

- Edge-device monitoring
- Microservice observability
- Integrated code-quality visibility
- CI/CD workflow transparency
- Engineering analytics
- Business-friendly reporting
- Educational accessibility
- Lightweight deployment
- A single project-oriented data model

The combination of Raspberry Pi monitoring and software engineering operations is a distinctive product direction.

---

## 18. Version 2.0 Sprint Alignment

| Sprint | Epic | Strategic Outcome |
|---|---|---|
| Sprint 7 | Advanced Observability Platform | Establish project and observability foundations |
| Sprint 8 | Intelligent Alerting Platform | Improve detection, notification and response |
| Sprint 9 | Edge Device Management Platform | Extend the working Raspberry Pi platform into fleet management |
| Sprint 10 | Analytics and Reporting Platform | Convert technical data into engineering and business insight |
| Sprint 11 | DevOps and SaaS Platform | Introduce repository, CI/CD and code-quality capabilities |
| Sprint 12 | Enterprise Platform | Introduce organisations, permissions, governance and tenant foundations |

---

## 19. Long-Term Direction

Future versions may introduce:

- AI-assisted root-cause analysis
- Predictive failure detection
- Natural-language operational queries
- Automated incident summaries
- Pipeline recommendations
- Quality-improvement recommendations
- Kubernetes integration
- Public cloud integration
- Advanced tenant billing
- Marketplace integrations
- Mobile operational views
- Remote edge deployment
- Automated remediation with approval controls

These features must build on reliable Version 2.0 data and governance foundations.

---

## 20. Vision Approval Criteria

This product vision is ready for approval when:

- Version 1.0 continuity is clearly protected.
- The Version 2.0 user groups are agreed.
- The Jenkins and SonarQube replacement strategy is understood as incremental.
- Raspberry Pi support remains first-class.
- The project-oriented platform model is accepted.
- The six Version 2.0 epics align with the product direction.
- The initial scope and exclusions are understood.
- Product success measures are measurable.
- Architecture and requirements planning can proceed from this vision.

---

## 21. Current Approval Status

Status: Draft

Prepared for: EdgeCloud Platform Version 2.0 planning

Owner: Taha Aflouk

Next document: `VERSION_2_PRODUCT_REQUIREMENTS.md`
