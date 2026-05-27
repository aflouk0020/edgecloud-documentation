# WEEK 02 PROGRESS REPORT  
## EdgeCloud Monitor – Infrastructure and Service Discovery

### Overview
During Week 02, the core cloud-native infrastructure layer for the EdgeCloud Monitor platform was expanded significantly. The primary focus of this phase was the implementation and validation of Netflix Eureka service discovery together with Spring Cloud API Gateway integration.

This work established the foundation required for dynamic service registration, service resolution, centralised routing, and distributed microservice communication.

---

# Objectives Completed

- Configured Netflix Eureka Discovery Server
- Configured Eureka client registration
- Integrated Spring Cloud API Gateway
- Validated service registration workflow
- Implemented API Gateway health endpoint
- Verified dynamic service discovery
- Configured actuator health monitoring
- Validated graceful service shutdown and deregistration
- Completed GitHub feature branch workflow
- Completed Pull Request merge workflow
- Organised project evidence and screenshots

---

# Discovery Service Implementation

## Technologies Used

- Java 21
- Spring Boot 3.5.x
- Spring Cloud Netflix Eureka Server
- Maven
- Docker
- GitHub

## Completed Tasks

### Eureka Server Configuration
The Discovery Service was configured as a Netflix Eureka Server to support service registration and distributed service lookup across the platform.

Key implementation steps included:

- Creating the Spring Boot Discovery Service project
- Adding Eureka Server dependency
- Enabling Eureka Server using `@EnableEurekaServer`
- Configuring application YAML properties
- Running the Eureka dashboard on port `8761`

### Eureka Dashboard Validation

The Eureka dashboard was successfully validated through browser testing.

Verified URL:

```text
http://localhost:8761
```

The dashboard displayed:

- System status
- Registered services
- Availability zones
- Instance information

---

# API Gateway Integration

## API Gateway Configuration

The API Gateway was configured using Spring Cloud Gateway MVC.

Configured routes:

| Route | Target Service |
|---|---|
| `/api/v1/auth/**` | Authentication Service |
| `/api/v1/monitoring/**` | Monitoring Service |
| `/api/v1/devices/**` | Device Service |
| `/api/v1/alerts/**` | Alert Service |

---

# Eureka Client Registration

The API Gateway was successfully registered with Eureka using the following configuration:

```yaml
eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
```

The Eureka dashboard confirmed successful registration of:

```text
EDGECLOUD-API-GATEWAY
```

---

# Health Monitoring Implementation

## Gateway Health Endpoint

A custom health monitoring controller was implemented.

Example endpoint:

```text
/gateway/status
```

The endpoint was successfully tested and returned healthy application status information.

---

# Actuator Integration

Spring Boot Actuator was configured to expose operational endpoints for monitoring and debugging.

Configured endpoints:

```yaml
management:
  endpoints:
    web:
      exposure:
        include: health,info
```

Validated endpoint:

```text
http://localhost:8080/actuator/health
```

Expected response:

```json
{
  "status": "UP"
}
```

---

# Dynamic Service Discovery Validation

The API Gateway successfully communicated with Eureka and dynamically registered itself during startup.

Validation evidence included:

- Successful Eureka registration logs
- Registration status `204`
- Service visibility inside Eureka dashboard
- Successful deregistration during shutdown
- Graceful shutdown confirmation logs

---

# Git and GitHub Workflow

Professional Git workflow practices were followed throughout development.

## Completed Workflow

- Created feature branches
- Implemented isolated development changes
- Committed changes using structured commit messages
- Pushed branches to GitHub
- Created Pull Requests
- Merged Pull Requests into `main`
- Deleted merged branches

Example commit message:

```text
feat(gateway): add gateway health status endpoint
```

---

# Technical Challenges Encountered

## Java Runtime Version Conflict

An issue occurred where Maven attempted to run Spring Boot using an older Java runtime.

### Cause
The terminal session was using Java 11 instead of Java 21.

### Resolution
The environment was updated to Java 21 before running Maven commands.

Validated version:

```text
Java 21
```

---

## Gateway Route Configuration Issue

An issue occurred with actuator route exposure and incorrect Spring Cloud Gateway configuration structure.

### Resolution

The gateway configuration was updated to the correct Spring Cloud Gateway MVC structure.

---

# Evidence Collected

The following evidence was collected during implementation:

- Eureka dashboard screenshots
- Gateway health endpoint screenshots
- Maven build logs
- Eureka registration logs
- GitHub Pull Request screenshots
- Git merge confirmation screenshots
- API response screenshots

Evidence was organised into the documentation structure for future reporting and presentation usage.

---

# Current Platform Status

The following infrastructure components are now operational:

| Component | Status |
|---|---|
| Eureka Discovery Service | Operational |
| API Gateway | Operational |
| Eureka Client Registration | Operational |
| Gateway Health Monitoring | Operational |
| GitHub Workflow | Operational |

---

# Next Planned Activities

Upcoming implementation tasks include:

- Authentication Service development
- JWT security integration
- Monitoring Service implementation
- Device Service implementation
- Alert Service implementation
- Docker Compose integration
- Multi-service routing validation

---

# Conclusion

Week 02 successfully established the foundational cloud-native infrastructure layer required for the EdgeCloud Monitor platform.

The implementation validated dynamic service discovery, distributed service registration, centralised API routing, and operational health monitoring. These components now provide the base architecture required for the remaining backend microservices and observability workflows.