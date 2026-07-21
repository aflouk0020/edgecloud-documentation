# EdgeCloud Monitor
## Master Development Plan

---

# 1. Project Overview

EdgeCloud Monitor is a cloud-native monitoring platform designed to monitor distributed microservices and edge devices from a unified dashboard.

The platform will collect telemetry and health information from backend services, APIs, Docker containers, databases, and Raspberry Pi edge devices in order to improve observability, fault detection, and operational visibility across distributed environments.

The system is being developed as part of the MSc Work Placement and Professional Practice module at Technological University of the Shannon (TUS).

---

# 2. Core Problem

Modern distributed systems introduce operational complexity that makes monitoring and fault detection difficult for smaller development teams and educational environments.

Existing enterprise monitoring solutions are often overly complex or fragmented across multiple tools.

This project aims to provide a lightweight, modular, and practical monitoring platform focused on:

- microservices monitoring
- edge device monitoring
- telemetry collection
- cloud-native deployment
- alerting and observability

---

# 3. Primary Project Goals

The project aims to:

- design a cloud-native monitoring architecture
- implement distributed backend services
- monitor service health and availability
- integrate edge telemetry collection
- visualise system health through dashboards
- implement alerting capabilities
- demonstrate cloud-native engineering practices
- apply microservices architecture principles
- demonstrate observability concepts

---

# 4. System Architecture Strategy

The project will follow a distributed microservices architecture.

Core architectural components include:

- API Gateway
- Service Discovery
- Authentication Service
- Monitoring Service
- Device Service
- Alert Service
- Dashboard Frontend
- Edge Telemetry Agent

The system will support communication between cloud services and edge devices using REST APIs.

---

# 5. Locked Technology Decisions

## Backend
- Java 21
- Spring Boot
- Maven

## Frontend
- React Dashboard

## Communication
- REST APIs

## Security
- JWT Authentication

## Cloud-Native Stack
- Docker
- Docker Compose
- Spring Cloud Gateway
- Netflix Eureka

## Databases
- MySQL
- Database-per-service architecture

## Edge Computing
- Raspberry Pi
- Python telemetry agent

## Version Control
- GitHub
- Git-based workflow

---

# 6. Development Methodology

The project will follow an iterative and incremental development approach.

Development will be divided into structured phases aligned with the placement module schedule.

Each phase will include:
- planning
- implementation
- testing
- documentation
- review

Weekly supervisor meetings and weekly logs will be used to track progress.

---

# 7. Planned Development Phases

## Phase 1 — Core Platform MVP
Target:
- establish backend infrastructure
- configure gateway and discovery
- implement authentication
- implement monitoring service
- establish Docker deployment
- develop initial dashboard

## Phase 2 — Edge Integration
Target:
- integrate Raspberry Pi telemetry
- implement heartbeat monitoring
- device registration
- telemetry storage

## Phase 3 — Smart Monitoring Features
Target:
- alert system
- historical metrics
- graph visualisation
- root-cause suggestions

## Phase 4 — Optional Extensions
Possible extensions:
- Kubernetes
- Android application
- AI anomaly detection
- CI/CD pipelines
- Prometheus integration
- real-time notifications

---

# 8. MVP Scope

The MVP will focus on the minimum system needed to demonstrate the main engineering value of EdgeCloud Monitor.

## MVP Includes

- API Gateway
- Eureka Discovery Service
- Authentication Service with JWT
- Monitoring Service
- Device Service
- Alert Service
- React Dashboard
- Docker Compose deployment
- simulated edge telemetry agent
- basic Raspberry Pi integration if time allows

## MVP Excludes

- Kubernetes
- Android application
- AI anomaly detection
- MQTT
- Prometheus integration
- advanced real-time streaming

These excluded features may be treated as optional future enhancements if time allows.
---

# 9. Repository Strategy

Each microservice will maintain an independent Git repository.

Planned repositories:

- edgecloud-api-gateway
- edgecloud-discovery-service
- edgecloud-auth-service
- edgecloud-monitoring-service
- edgecloud-device-service
- edgecloud-alert-service
- edgecloud-dashboard
- edgecloud-edge-agent
- edgecloud-documentation

This structure supports:
- service isolation
- scalability
- independent deployment
- professional engineering workflow

---

# 10. Infrastructure Strategy

The platform will initially be deployed locally using Docker Compose.

The infrastructure will include:
- container networking
- service discovery
- gateway routing
- database containers
- isolated services

Cloud deployment may later be explored using:
- Render
- Railway
- AWS
- Azure

---

# 11. Timeline Alignment

The project timeline will align with the MSc Work Placement and Professional Practice module schedule.

Key dates:

| Milestone | Date |
|---|---|
| Project start date | 18 May 2026 |
| MVP target completion | Before 21 June 2026 |
| Interim report and presentation deadline | 5 July 2026 |
| Final report and presentation deadline | 23 August 2026 |

The MVP phase must be completed before the interim submission deadline so that the interim report and presentation include strong technical evidence.
---

# 12. Documentation Strategy

The project will maintain structured documentation throughout development.

Documentation will include:
- architecture diagrams
- API documentation
- deployment documentation
- sprint plans
- risk management
- testing evidence
- screenshots
- meeting notes
- weekly progress tracking

Evidence will be collected weekly, including screenshots, Git commits, Docker logs, Postman results, Eureka dashboard screenshots, API responses, frontend dashboard screenshots, testing results, and deployment evidence.

---

# 13. Risk Management

Potential risks include:
- project scope expansion
- infrastructure complexity
- integration challenges
- deployment issues
- time constraints
- edge communication failures

Mitigation strategies:
- phased implementation
- MVP-first strategy
- weekly progress reviews
- controlled feature expansion

---

# 14. Expected Outcomes

The final system should demonstrate:
- cloud-native engineering
- distributed systems design
- microservices implementation
- observability concepts
- edge computing integration
- monitoring and alerting
- backend engineering
- deployment engineering

---

# 15. Future Potential

The project may later evolve into:
- a larger observability platform
- industrial edge monitoring system
- research continuation
- portfolio project
- deployment-ready monitoring solution

---