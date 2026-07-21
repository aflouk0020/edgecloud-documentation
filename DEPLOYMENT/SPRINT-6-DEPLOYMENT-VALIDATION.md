# Sprint 6 Deployment Validation Summary

## 1. Overview

Sprint 6 included deployment validation activities to confirm that the EdgeCloud Monitor cloud-native architecture remained stable after introducing additional monitoring, analytics, alerting, and performance testing capabilities.

The objective was to ensure that the distributed platform could be deployed consistently using Docker Compose while maintaining reliable communication between independent services.

---

# 2. Deployment Environment

The platform was validated using the local Docker Compose deployment environment.

Environment:

- Operating System: macOS
- Container Platform: Docker Compose
- Backend Framework: Spring Boot Microservices
- Frontend: React Dashboard
- Databases: MySQL containers
- Service Discovery: Netflix Eureka
- Communication: REST APIs

---

# 3. Validated Services

The following services were validated during deployment testing:

## API Gateway

Responsibilities:

- Centralised API entry point.
- Request routing.
- Communication between frontend and backend services.

---

## Discovery Service

Responsibilities:

- Service registration.
- Service availability tracking.
- Microservice discovery.

---

## Authentication Service

Responsibilities:

- User authentication.
- JWT token generation.
- Access control.

---

## Monitoring Service

Responsibilities:

- Service health monitoring.
- Telemetry processing.
- Metrics storage.
- Analytics generation.

---

## Device Service

Responsibilities:

- Edge device registration.
- Device status management.
- Heartbeat tracking.

---

## Alert Service

Responsibilities:

- Alert creation.
- Incident workflow preparation.
- Alert lifecycle management.

---

# 4. Docker Validation Results

Deployment testing confirmed:

- Containers started successfully.
- Services communicated through Docker networking.
- Database containers remained available.
- Environment configuration was loaded correctly.
- Backend services operated independently.

---

# 5. Infrastructure Stability Outcome

Sprint 6 deployment validation demonstrated that the EdgeCloud Monitor infrastructure remained stable while additional monitoring and operational features were introduced.

The deployment architecture continues to follow cloud-native principles:

- Independent services.
- Containerised deployment.
- Environment-based configuration.
- API-driven communication.
- Service isolation.

---

# 6. Future Work

(To be defined after project review)
