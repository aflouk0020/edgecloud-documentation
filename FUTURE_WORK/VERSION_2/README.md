# EdgeCloud Platform Version 2.0 Planning Documentation

## 1. Purpose

This directory contains the authoritative planning documentation for EdgeCloud Platform Version 2.0.

Version 2.0 evolves EdgeCloud Monitor from a cloud-native edge-device monitoring platform into a broader Engineering Operations Platform that supports software development teams, DevOps engineers, technical managers, students and organisations operating distributed software systems.

The planning material in this directory must be completed and reviewed before Version 2.0 implementation begins.

## 2. Version 1.0 Baseline

EdgeCloud Monitor Version 1.0 is the completed platform baseline.

It currently provides:

- Spring Boot microservice architecture
- Netflix Eureka service discovery
- API Gateway routing
- JWT authentication and role-based access control
- Monitoring Service
- Device Service
- Alert Service
- React dashboard
- Raspberry Pi edge telemetry agent
- Historical metric collection
- Threshold-based alerting
- Docker Compose deployment
- Testing, documentation and deployment validation

Version 2.0 must extend this baseline without breaking existing edge-device monitoring, Raspberry Pi telemetry, authentication, alerts, dashboard workflows or Docker deployment.

## 3. Version 2.0 Product Direction

Version 2.0 will expand EdgeCloud into a unified platform for:

- Microservice monitoring
- Application performance visibility
- Raspberry Pi and edge-device monitoring
- CI/CD workflow visibility
- Build and deployment tracking
- Source-code quality reporting
- Quality gates
- Test coverage reporting
- Technical debt and complexity indicators
- Alerting and notifications
- Engineering analytics
- Incident management
- Organisation and user governance
- Future SaaS operation

The platform is intended to combine capabilities commonly distributed across monitoring, CI/CD, code-quality and engineering analytics tools.

The objective is not to immediately reproduce every feature of Jenkins, SonarQube, Grafana or commercial observability platforms. Version 2.0 will introduce focused, practical capabilities that are achievable, secure and valuable for smaller teams, start-ups, educational environments and distributed edge deployments.

## 4. Target Users

Version 2.0 is designed for:

- Software developers
- DevOps engineers
- Platform engineers
- Technical managers
- Small development teams
- Start-ups
- University project teams
- Students learning cloud-native development
- Organisations operating microservices
- Teams managing Raspberry Pi and edge devices

## 5. Version 2.0 Jira Structure

The Version 2.0 Jira roadmap contains the following epics and sprints.

| Sprint | Epic | Product Area |
|---|---|---|
| Sprint 7 | Advanced Observability Platform | Microservice monitoring, metrics and observability foundation |
| Sprint 8 | Intelligent Alerting Platform | Alert rules, notifications, acknowledgement and escalation |
| Sprint 9 | Edge Device Management Platform | Raspberry Pi and edge-fleet management |
| Sprint 10 | Analytics and Reporting Platform | Dashboards, trends, reports and engineering insights |
| Sprint 11 | DevOps and SaaS Platform | Repository integration, CI/CD, code quality and automation |
| Sprint 12 | Enterprise Platform | Multi-tenancy, organisations, permissions and governance |

All stories must be linked to:

- The correct epic
- The correct sprint
- The EdgeCloud Monitor v2.0 release
- Appropriate labels
- The correct technical component
- Relevant dependencies

## 6. Planning Documents

The documents in this directory must be completed in the following order.

1. `README.md`
2. `VERSION_2_PRODUCT_VISION.md`
3. `VERSION_2_PRODUCT_REQUIREMENTS.md`
4. `VERSION_2_PLATFORM_ARCHITECTURE.md`
5. `VERSION_2_JIRA_ROADMAP.md`
6. `VERSION_2_STORY_STANDARD.md`
7. `VERSION_2_ENGINEERING_STANDARDS.md`
8. `VERSION_2_RISK_ASSESSMENT.md`
9. `VERSION_2_DEPENDENCY_MATRIX.md`
10. `VERSION_2_DATABASE_PLAN.md`
11. `VERSION_2_API_PLAN.md`
12. `VERSION_2_UI_UX_PLAN.md`

## 7. Story Quality Standard

Every Version 2.0 story must include:

- Issue type
- Summary
- User story
- Business value
- Detailed description
- Acceptance criteria
- Definition of Done
- Story points
- Priority
- Epic
- Sprint
- Fix version
- Labels
- Component
- Dependencies
- Technical notes
- Testing requirements
- Security considerations
- Documentation requirements
- Evidence requirements

No implementation story should enter an active sprint until it satisfies the agreed Definition of Ready.

## 8. Engineering Principles

Version 2.0 development must follow these principles:

- Preserve Version 1.0 functionality.
- Avoid direct cross-service database access.
- Maintain clear service ownership.
- Use API-driven communication.
- Reuse existing services before creating new microservices.
- Introduce new domain services only when architectural boundaries justify them.
- Keep Raspberry Pi support as a first-class capability.
- Apply secure defaults.
- Never expose secrets, tokens or webhook signatures.
- Use feature branches and pull requests.
- Build and test after each significant change.
- Keep the main branch stable.
- Document all architecture and API changes.
- Record evidence for completed stories.
- Avoid overstating unfinished functionality.
- Introduce complex capabilities incrementally.

## 9. Product Governance

Version 1.0 remains the historical MSc release and must not be rewritten.

Version 2.0 work must be recorded separately through:

- Version 2.0 Jira epics
- Version 2.0 sprints
- Version 2.0 documentation
- Version 2.0 branches and pull requests
- Version 2.0 testing evidence
- Version 2.0 architecture decisions

Any change that risks breaking Version 1.0 must include:

- Regression testing
- Migration planning
- Rollback planning
- Compatibility assessment
- Updated documentation

## 10. Implementation Gate

Version 2.0 implementation may begin only when:

- Product vision is approved
- Product requirements are documented
- Architecture direction is reviewed
- Jira roadmap is approved
- Story format is standardised
- Engineering standards are defined
- Risks are assessed
- Dependencies are mapped
- Database ownership is agreed
- API design is outlined
- UI and UX direction is documented
- Sprint 7 stories meet the Definition of Ready

## 11. Current Status

- Version 1.0 completed
- Version 2.0 release created in Jira
- Version 2.0 epics created
- Sprints 7 through 12 created
- Version 2.0 planning directory created
- Detailed planning documents pending completion
- No Version 2.0 implementation started
