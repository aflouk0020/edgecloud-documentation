# EdgeCloud Monitor
## Development Roadmap

---

# 1. Introduction

This document defines the development execution roadmap for the EdgeCloud Monitor project.

The roadmap aligns technical implementation with the MSc Work Placement and Professional Practice module timeline at Technological University of the Shannon (TUS).

The roadmap aims to:

- provide structured engineering execution
- protect MVP delivery
- support weekly progress tracking
- align implementation with academic deadlines
- support professional software engineering practices
- ensure continuous documentation and evidence collection

The project will follow an MVP-first engineering strategy.

---

# 2. Placement Timeline

| Milestone | Date |
|---|---|
| Placement Start | 18 May 2026 |
| MVP Target Completion | Before 21 June 2026 |
| Interim Report + Presentation | 5 July 2026 |
| Final Submission + Presentation | 23 August 2026 |

---

# 3. Development Strategy

The project will follow an iterative phased development approach.

Each phase includes:

- planning
- implementation
- testing
- documentation
- deployment validation
- evidence collection

The implementation order prioritises:

1. infrastructure stability
2. service communication
3. authentication
4. monitoring functionality
5. frontend visualisation
6. edge integration
7. alerting and observability improvements
8. optional enhancements

---

# 4. Engineering Workflow Strategy

The project will follow professional engineering practices throughout development.

## Planned Workflow

- GitHub-based version control
- independent repositories per service
- feature branch workflow
- incremental Docker integration
- API-first development
- continuous documentation updates
- weekly supervisor review cycle
- continuous evidence collection

---

# 5. Repository Creation Order

Repositories will be created in the following order:

| Priority | Repository |
|---|---|
| 1 | edgecloud-discovery-service |
| 2 | edgecloud-api-gateway |
| 3 | edgecloud-auth-service |
| 4 | edgecloud-monitoring-service |
| 5 | edgecloud-device-service |
| 6 | edgecloud-alert-service |
| 7 | edgecloud-dashboard |
| 8 | edgecloud-edge-agent |
| 9 | edgecloud-documentation |

---

# 6. Planned Development Phases

---

# Phase 1 — Foundation and Infrastructure

## Target Period

18 May 2026 → 24 May 2026

---

## Main Objectives

- establish repository structure
- configure development environments
- implement Discovery Service
- implement API Gateway
- establish Docker networking
- validate service communication

---

## Planned Tasks

### Infrastructure

- create GitHub repositories
- configure Maven projects
- configure Dockerfiles
- configure Docker Compose
- create shared Docker network
- configure Eureka Discovery Server
- configure Spring Cloud Gateway

### Validation

- validate service registration
- validate gateway routing
- validate Docker networking
- test container startup order

### Documentation

- update architecture diagrams
- capture Eureka screenshots
- capture Docker deployment evidence
- document infrastructure setup

---

## Deliverables

- working Discovery Service
- working API Gateway
- Docker Compose baseline
- initial infrastructure evidence

---

# Phase 2 — Authentication and Core Backend Services

## Target Period

25 May 2026 → 31 May 2026

---

## Main Objectives

- implement Authentication Service
- implement JWT security
- establish database containers
- configure MySQL integration
- implement Monitoring Service baseline

---

## Planned Tasks

### Authentication Service

- user registration
- login endpoint
- JWT generation
- JWT validation
- password hashing
- protected routes

### Monitoring Service

- monitored service registration
- health status APIs
- telemetry ingestion APIs
- database persistence

### Database Work

- configure auth_db
- configure monitoring_db
- validate database isolation

### Testing

- Postman API testing
- JWT validation testing
- service-to-service communication testing

### Documentation

- capture authentication flow evidence
- capture Postman screenshots
- document JWT architecture

---

## Deliverables

- functional Authentication Service
- functional Monitoring Service baseline
- JWT-secured APIs
- isolated database infrastructure

---

# Phase 3 — Device Management and Edge Telemetry

## Target Period

1 June 2026 → 7 June 2026

---

## Main Objectives

- implement Device Service
- implement edge telemetry agent
- establish heartbeat monitoring
- integrate Raspberry Pi telemetry flow

---

## Planned Tasks

### Device Service

- device registration APIs
- heartbeat APIs
- device status management
- device database integration

### Edge Agent

- Python telemetry agent
- CPU monitoring
- memory monitoring
- temperature monitoring
- REST telemetry submission

### Integration

- telemetry ingestion validation
- heartbeat validation
- edge disconnect simulation

### Testing

- simulated telemetry testing
- Raspberry Pi testing
- Docker integration testing

### Documentation

- telemetry screenshots
- API evidence
- telemetry logs
- device registration evidence

---

## Deliverables

- working Device Service
- working telemetry agent
- successful telemetry ingestion
- heartbeat monitoring

---

# Phase 4 — Alert System and Monitoring Features

## Target Period

8 June 2026 → 14 June 2026

---

## Main Objectives

- implement Alert Service
- implement failure detection
- implement monitoring logic
- establish observability features

---

## Planned Tasks

### Alert Service

- alert generation
- alert retrieval APIs
- alert resolution APIs
- alert persistence

### Monitoring Logic

- service failure detection
- latency threshold monitoring
- device offline detection
- basic root-cause suggestions

### Failure Simulations

- stop containers
- simulate latency
- disconnect devices
- simulate failed services

### Documentation

- alert screenshots
- observability diagrams
- failure evidence
- monitoring logs

---

## Deliverables

- working Alert Service
- monitoring rule engine
- observable failure detection
- alert visualisation APIs

---

# Phase 5 — React Dashboard Development

## Target Period

15 June 2026 → 21 June 2026

---

## Main Objectives

- implement React frontend
- visualise monitoring data
- integrate backend APIs
- complete MVP functionality

---

## Planned Tasks

### Frontend Features

- login page
- dashboard layout
- service status cards
- telemetry display
- alert display
- device monitoring views

### API Integration

- JWT integration
- API Gateway integration
- monitoring APIs
- device APIs
- alert APIs

### UI Validation

- dashboard refresh testing
- alert visualisation testing
- authentication testing

### Documentation

- dashboard screenshots
- integration evidence
- MVP architecture evidence

---

## Deliverables

- functional React dashboard
- integrated monitoring platform
- MVP completion

---

# 7. MVP Completion Milestone

## Target Date

Before 21 June 2026

---

## MVP Completion Criteria

The MVP is considered complete when:

- all core services run successfully
- services register with Eureka
- API Gateway routing functions correctly
- JWT authentication operates correctly
- telemetry is received and stored
- alerts are generated during failures
- dashboard visualises monitoring data
- Docker Compose deployment operates reliably
- edge telemetry communication functions correctly

---

# 8. Interim Submission Preparation

## Target Period

22 June 2026 → 5 July 2026

---

## Main Objectives

- stabilise MVP
- improve documentation quality
- prepare interim report
- prepare interim presentation
- collect professional evidence

---

## Planned Tasks

### Documentation

- refine architecture diagrams
- refine deployment diagrams
- update API documentation
- update testing evidence
- finalise interim screenshots

### Presentation Preparation

- deployment demonstrations
- Docker evidence
- monitoring demonstrations
- telemetry demonstrations

### Testing

- repeat integration testing
- verify deployment reliability
- validate monitoring flows

---

## Deliverables

- interim report
- interim presentation
- stable MVP demonstration

---

# 9. Phase 6 — Advanced Improvements and Platform Refinement

## Target Period

6 July 2026 → 2 August 2026

---

## Main Objectives

- improve platform reliability
- improve dashboard quality
- improve observability
- add optional engineering enhancements

---

## Planned Improvements

### Backend Improvements

- improved monitoring logic
- better alert handling
- API optimisation
- structured logging improvements

### Frontend Improvements

- charts and graphs
- improved UI styling
- responsive dashboard improvements

### Infrastructure Improvements

- Docker optimisation
- health checks
- improved environment configuration

### Optional Extensions

- Prometheus integration
- GitHub Actions CI/CD
- Kubernetes exploration
- advanced metrics visualisation

---

## Deliverables

- refined platform
- improved engineering quality
- enhanced observability features

---

# 10. Finalisation and Submission Preparation

## Target Period

3 August 2026 → 23 August 2026

---

## Main Objectives

- finalise documentation
- complete final report
- prepare final presentation
- validate deployment stability
- organise engineering evidence

---

## Planned Tasks

### Final Documentation

- final architecture diagrams
- final deployment evidence
- testing evidence consolidation
- final screenshots
- GitHub repository organisation

### Final Validation

- full system deployment testing
- Docker validation
- edge telemetry validation
- alert validation
- dashboard validation

### Presentation Preparation

- demonstration workflow
- failure simulation demonstrations
- observability demonstrations
- telemetry demonstrations

---

## Deliverables

- final report
- final presentation
- complete deployment evidence
- portfolio-quality project repositories

---

# 11. Weekly Progress Tracking Strategy

Weekly logs will include:

- completed tasks
- blockers and issues
- screenshots and evidence
- infrastructure progress
- testing progress
- deployment progress
- next-week objectives

Weekly supervisor meetings will be used to:

- review progress
- validate milestones
- control project scope
- adjust priorities where necessary

---

# 12. Evidence Collection Strategy

Evidence will be collected continuously throughout development.

## Planned Evidence Types

- GitHub commits
- architecture diagrams
- Docker logs
- Eureka dashboard screenshots
- Postman API tests
- React dashboard screenshots
- telemetry logs
- alert screenshots
- deployment screenshots
- testing evidence

This evidence will support:

- weekly Moodle submissions
- interim report
- interim presentation
- final report
- final presentation

---

# 13. Risk-Control Alignment

The roadmap follows an MVP-first strategy to reduce project risk.

Key protections include:

- infrastructure-first implementation
- incremental Docker integration
- simple initial monitoring logic
- phased frontend development
- optional advanced features
- continuous testing and documentation

Advanced technologies such as Kubernetes and AI anomaly detection remain optional and will only be explored if the MVP is fully stable.

---

# 14. Expected Final Outcome

The final platform should demonstrate:

- cloud-native engineering
- distributed systems architecture
- Docker-based deployment
- microservice communication
- JWT security integration
- observability principles
- edge telemetry monitoring
- monitoring dashboard visualisation
- alert generation
- professional software engineering workflow

---

# 15. Conclusion

This roadmap provides a structured execution strategy for EdgeCloud Monitor aligned with MSc placement timelines and professional engineering practices.

The phased approach prioritises:

- MVP protection
- infrastructure stability
- modular engineering
- continuous testing
- continuous documentation
- deployment validation
- professional evidence collection

while maintaining flexibility for optional future enhancements and platform refinement.