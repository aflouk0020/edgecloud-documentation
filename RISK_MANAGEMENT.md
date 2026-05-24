# EdgeCloud Monitor
## Risk Management Plan

---

# 1. Introduction

This document identifies the main risks associated with the development of EdgeCloud Monitor and outlines mitigation strategies.

The project involves multiple technical areas including microservices, Docker, API Gateway routing, service discovery, databases, React dashboard development, and Raspberry Pi edge telemetry.

Because of this, risk management is important to keep the project realistic, achievable, and aligned with the placement timeline.

---

# 2. Risk Management Approach

Risks will be managed using the following approach:

- identify risks early
- assess likelihood and impact
- define mitigation actions
- review risks during weekly progress checks
- keep the MVP scope protected
- move advanced features to optional extensions where necessary

The project will follow an MVP-first strategy to reduce delivery risk.

---

# 3. Risk Summary Table

| ID | Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|---|
| R1 | Project scope becomes too large | High | High | Prioritise MVP features and keep advanced features optional |
| R2 | Too many microservices increase complexity | Medium | High | Start with core services only and avoid unnecessary service expansion |
| R3 | Docker networking issues | Medium | High | Build Docker Compose incrementally and test one service at a time |
| R4 | API Gateway routing problems | Medium | Medium | Configure routes early and document gateway paths clearly |
| R5 | Eureka service discovery issues | Medium | Medium | Test service registration before adding business logic |
| R6 | JWT authentication integration delays | Medium | Medium | Implement authentication early and keep security flow simple |
| R7 | Database-per-service design adds overhead | Medium | Medium | Use simple schemas and avoid cross-service database dependencies |
| R8 | Raspberry Pi telemetry integration becomes unstable | Medium | High | Begin with simulated telemetry before using physical device data |
| R9 | React dashboard takes longer than expected | Medium | Medium | Build simple dashboard first, then add charts and polish later |
| R10 | Alert and root-cause logic becomes too complex | Medium | Medium | Start with simple rule-based suggestions only |
| R11 | Kubernetes deployment takes too much time | High | Medium | Treat Kubernetes as optional future work |
| R12 | Final report and presentation evidence is incomplete | Medium | High | Capture screenshots, diagrams, logs, and weekly notes continuously |
| R13 | Time pressure before interim submission | High | High | Complete MVP before 21 June and reserve final week before interim for polishing |
| R14 | Edge device hardware unavailable or difficult to configure | Medium | Medium | Use a simulated edge agent as fallback |
| R15 | Integration between services becomes difficult | Medium | High | Define API contracts early and test each service independently |
| R16 | Environment configuration inconsistencies | Medium | Medium | Use structured environment variables and documented configuration management |
| R17 | Service startup dependency failures | Medium | Medium | Use Docker health checks and controlled startup ordering |
| R18 | Insufficient testing coverage | Medium | High | Apply layered testing and continuous integration testing practices |

---

# 4. Detailed Risk Analysis

## R1 — Project Scope Becomes Too Large

### Description

The project includes several technical areas such as microservices, Docker, React, edge telemetry, monitoring, alerts, and potential cloud deployment.

There is a risk of adding too many features too early.

### Impact

This could lead to unfinished features, unstable implementation, and weak final delivery.

### Mitigation

The project will follow an MVP-first approach.

Core features will be prioritised before optional features such as:

- Kubernetes
- AI anomaly detection
- Android application
- MQTT
- Prometheus integration

---

## R2 — Microservice Complexity

### Description

Multiple repositories and services increase development, configuration, and testing complexity.

### Impact

Service communication, debugging, and deployment may become difficult.

### Mitigation

Only core services will be implemented initially:

- API Gateway
- Discovery Service
- Authentication Service
- Monitoring Service
- Device Service
- Alert Service
- React Dashboard
- Edge Agent

Additional services will only be added if time allows.

---

## R3 — Docker Networking Issues

### Description

Docker networking can cause problems when services need to communicate using container names, ports, and internal networks.

### Impact

Services may fail to connect to each other, databases, or the API Gateway.

### Mitigation

Docker Compose will be built incrementally.

Each service will be tested individually before full integration.

A dedicated Docker network will be used and documented.

---

## R4 — API Gateway Routing Problems

### Description

Incorrect gateway configuration can prevent frontend requests from reaching backend services.

### Impact

The system may appear broken even when backend services are running correctly.

### Mitigation

Gateway routes will be defined early and documented in the API specification.

Routes will be tested using Postman before frontend integration.

---

## R5 — Eureka Service Discovery Issues

### Description

Services may fail to register correctly with Eureka due to configuration or networking problems.

### Impact

Dynamic routing and service discovery may not work correctly.

### Mitigation

Eureka will be implemented and tested early before adding advanced functionality.

Service registration screenshots will be captured for documentation evidence.

---

## R6 — JWT Authentication Integration Delays

### Description

Authentication and token validation can create delays, especially when integrated through an API Gateway and React frontend.

### Impact

Protected routes may block progress on other system features.

### Mitigation

Authentication will be kept simple in the MVP.

Basic login, token generation, and token validation will be implemented first.

Role-based access can be expanded later.

---

## R7 — Database-Per-Service Overhead

### Description

Using a separate database per service improves architecture quality but increases setup and configuration effort.

### Impact

Database configuration may slow development.

### Mitigation

Database schemas will be kept simple.

No cross-service foreign keys will be used.

Services will communicate through APIs rather than shared databases.

---

## R8 — Raspberry Pi Telemetry Instability

### Description

Physical edge device integration may introduce issues such as network instability, Python dependency problems, or hardware limitations.

### Impact

Edge monitoring may become unreliable or delay delivery.

### Mitigation

A simulated edge telemetry agent will be built first.

Raspberry Pi integration will then be added after the backend telemetry APIs are stable.

---

## R9 — React Dashboard Delay

### Description

Dashboard development may take longer than expected due to API integration, charting, and UI design.

### Impact

The project may lack visible output for interim or final presentation.

### Mitigation

A simple dashboard will be built first showing:

- service status
- device status
- alerts

Advanced charts and UI polish will be added later.

---

## R10 — Alert and Root-Cause Logic Complexity

### Description

Advanced root-cause analysis can become difficult if it requires complex log correlation or AI-based anomaly detection.

### Impact

This could make the project too large.

### Mitigation

The system will use simple rule-based logic for the MVP.

Example:

```text
High API latency + high database latency
→ probable database bottleneck
```

AI anomaly detection will remain optional.

---

## R11 — Kubernetes Complexity

### Description

Kubernetes deployment can be time-consuming and may distract from core implementation.

### Impact

Core project delivery may suffer if Kubernetes is attempted too early.

### Mitigation

Docker Compose will be the primary deployment method.

Kubernetes will be treated as an optional extension after the core system is complete.

---

## R12 — Missing Evidence for Reports

### Description

The placement module requires:

- weekly logs
- interim presentation
- interim report
- final presentation
- final report

If screenshots and notes are not collected throughout development, report writing becomes difficult.

### Impact

Academic deliverables may be weaker.

### Mitigation

Evidence will be collected weekly, including:

- screenshots
- architecture diagrams
- Git commits
- Docker logs
- dashboard screenshots
- meeting notes
- testing results
- deployment evidence
- API testing evidence

---

## R13 — Interim Deadline Pressure

### Description

The interim report and presentation are due on 5 July 2026.

### Impact

If the MVP is not ready before this date, the interim submission may lack strong technical evidence.

### Mitigation

The MVP target date is set before 21 June 2026.

The final week before interim submission will be reserved for:

- polishing
- screenshots
- diagrams
- presentation preparation
- deployment validation

---

## R14 — Edge Hardware Availability

### Description

Raspberry Pi hardware may be unavailable, unstable, or difficult to configure.

### Impact

Edge integration may be delayed.

### Mitigation

A Python-based simulated edge agent will be implemented first and can be used as a fallback if physical device integration is delayed.

---

## R15 — Service Integration Difficulty

### Description

Independent services may become difficult to integrate if API contracts are unclear.

### Impact

Integration bugs may slow development.

### Mitigation

API contracts will be defined before implementation.

Postman testing and documentation will be used to validate service communication.

---

## R16 — Environment Configuration Inconsistencies

### Description

Different local and container environments may introduce inconsistent configuration behaviour.

### Impact

Services may behave differently across development and deployment environments.

### Mitigation

Environment variables and configuration files will be standardised and documented carefully.

Docker Compose configuration will be version controlled and validated regularly.

---

## R17 — Service Startup Dependency Failures

### Description

Microservices may fail to start correctly if dependent services or databases are unavailable.

### Impact

The platform may fail during deployment or testing.

### Mitigation

Docker health checks and startup ordering strategies will be implemented.

Infrastructure components will be tested incrementally.

---

## R18 — Insufficient Testing Coverage

### Description

Distributed systems may hide integration bugs if testing coverage is weak.

### Impact

Undetected issues may appear during demonstrations or deployment.

### Mitigation

The project will use layered testing including:

- unit testing
- integration testing
- API testing
- Docker testing
- frontend testing
- edge telemetry testing

Testing evidence will be collected continuously.

---

# 5. MVP Protection Strategy

The MVP will focus only on the minimum required system needed to demonstrate the core project idea.

## MVP Includes

- service discovery
- API Gateway
- Authentication Service
- Monitoring Service
- Device Service
- Alert Service
- React Dashboard
- Docker Compose deployment
- REST-based edge telemetry
- simulated edge telemetry agent

## MVP Excludes

- Kubernetes
- Android application
- AI anomaly detection
- advanced Prometheus integration
- MQTT
- live log streaming

These excluded items may become future enhancements if time allows.

---

# 6. Risk Review Process

Risks will be reviewed during:

- weekly supervisor meetings
- weekly log preparation
- sprint planning
- milestone reviews
- interim preparation
- final preparation

Any major risk changes will be recorded in the project documentation.

---

# 7. Conclusion

Risk management is essential for keeping EdgeCloud Monitor realistic and achievable within the placement timeline.

The project will use:

- an MVP-first approach
- phased implementation
- controlled feature expansion
- continuous testing
- structured documentation
- incremental deployment

to reduce delivery risks and maintain strong engineering quality throughout development.