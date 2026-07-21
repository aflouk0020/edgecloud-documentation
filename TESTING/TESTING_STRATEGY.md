# EdgeCloud Monitor
## Testing Strategy

---

# 1. Introduction

This document defines the testing strategy for the EdgeCloud Monitor project.

The purpose of testing is to ensure that the platform remains stable, reliable, secure, and maintainable throughout development.

Because the project uses a distributed microservices architecture with cloud-native deployment and edge device integration, testing will be performed at multiple levels.

The testing process will focus on validating:

- backend services
- API communication
- authentication
- Docker deployment
- frontend integration
- edge telemetry
- service monitoring functionality
- alert generation
- system reliability

---

# 2. Testing Objectives

The main objectives of testing are:

- verify that services function correctly
- validate REST API communication
- ensure reliable service integration
- detect failures early
- reduce regression issues
- validate Docker deployment
- verify edge telemetry communication
- ensure dashboard functionality
- improve overall system stability

---

# 3. Testing Approach

The project will follow a layered testing strategy.

Testing will be divided into:

- unit testing
- integration testing
- API testing
- frontend testing
- deployment testing
- edge communication testing
- manual system testing

Testing will occur continuously throughout development rather than only at the end of the project.

---

# 4. Continuous Testing Strategy

Testing will be integrated throughout the full development lifecycle rather than performed only after implementation.

Continuous testing activities include:

- unit testing during development
- API verification after endpoint implementation
- Docker deployment validation after infrastructure changes
- frontend integration validation
- telemetry flow validation
- regression testing after major updates

This approach reduces integration risk and improves overall platform stability.

---

# 5. Testing Levels

---

# 5.1 Unit Testing

Unit testing will validate isolated components and business logic within individual services.

## Areas to Test

- service methods
- utility classes
- validation logic
- authentication logic
- telemetry processing logic
- alert generation rules

## Planned Tools

- JUnit 5
- Mockito

## Example Tests

- JWT token validation
- telemetry parsing
- alert rule triggering
- health status calculations
- database response handling

---

# 5.2 Integration Testing

Integration testing will verify communication between microservices and infrastructure components.

## Areas to Test

- API Gateway routing
- Eureka service discovery
- database communication
- service-to-service communication
- authentication flow across services

## Example Tests

- gateway forwarding requests correctly
- services registering with Eureka
- monitoring service storing telemetry data
- alert service receiving monitoring events

---

# 5.3 API Testing

REST APIs will be tested independently before frontend integration.

## Areas to Test

- endpoint responses
- request validation
- response codes
- JWT-protected routes
- invalid request handling

## Planned Tools

- Postman
- Swagger/OpenAPI documentation

## Example Tests

- valid login request
- invalid token rejection
- telemetry submission
- service status retrieval
- alert retrieval APIs

---

# 5.4 Frontend Testing

Frontend testing will validate dashboard functionality and API integration.

## Areas to Test

- dashboard rendering
- API data loading
- authentication flow
- charts and metrics display
- alert visualisation
- responsive behaviour

## Example Tests

- successful login
- dashboard refresh
- service health display
- telemetry graph updates
- alert display accuracy

---

# 5.5 Docker and Deployment Testing

Deployment testing will validate containerised infrastructure and cloud-native behaviour.

## Areas to Test

- Docker Compose deployment
- container networking
- service startup order
- environment configuration
- database container communication

## Example Tests

- services starting successfully
- containers communicating correctly
- database connectivity inside Docker network
- gateway routing inside containers

---

# 5.6 Health Check and Readiness Testing

Health and readiness testing will validate infrastructure stability and deployment reliability.

## Areas to Test

- Spring Boot actuator health endpoints
- database readiness
- Docker container health checks
- Eureka service registration
- API Gateway readiness

## Example Tests

- validating /actuator/health endpoints
- verifying healthy Docker containers
- ensuring services register with Eureka
- validating startup ordering behaviour

---

# 5.7 Edge Device Testing

Edge testing will validate communication between Raspberry Pi devices and backend services.

## Areas to Test

- telemetry transmission
- heartbeat communication
- edge device registration
- telemetry storage
- device disconnect handling

## Example Tests

- Raspberry Pi sending telemetry successfully
- heartbeat updates reaching backend
- system detecting edge disconnects
- telemetry data displayed in dashboard

---

# 5.8 System Testing

System testing will validate the complete integrated platform.

## Areas to Test

- full monitoring workflow
- authentication workflow
- alert generation workflow
- dashboard updates
- service failure detection
- edge monitoring workflow

## Example Scenarios

- stopping a Docker container
- disconnecting a database
- simulating API latency
- disconnecting edge device
- generating alert conditions

---

# 5.9 Observability Validation Testing

Because EdgeCloud Monitor is itself a monitoring platform, observability behaviour must also be validated.

## Areas to Test

- service health visibility
- telemetry visualisation
- alert visibility
- log generation
- dashboard updates
- monitoring accuracy

## Example Tests

- service failure appearing in dashboard
- telemetry graphs updating correctly
- alerts generated after simulated failures
- container status reflected accurately

---

# 6. Manual Testing Strategy

Manual testing will be used heavily during development.

Manual testing is important because the project includes:

- distributed services
- infrastructure behaviour
- UI visualisation
- telemetry flows
- real-time monitoring behaviour

Manual validation will include:

- API verification
- dashboard inspection
- Docker logs
- telemetry simulation
- container monitoring

---

# 7. Test Data Strategy

Testing will use controlled and repeatable test data where possible.

Example testing data includes:

- simulated telemetry payloads
- mock device registrations
- invalid authentication requests
- artificial API latency
- simulated container failures

This approach improves repeatability and debugging efficiency.

---

# 8. Test Environment

The project will use multiple environments during development.

## Local Development Environment

Used for:

- service development
- API testing
- unit testing

## Docker Environment

Used for:

- integration testing
- deployment testing
- service networking validation

## Edge Environment

Used for:

- Raspberry Pi telemetry testing
- edge communication validation

---

# 9. Error Simulation Strategy

The system will intentionally simulate failures to validate monitoring behaviour.

## Planned Simulations

- stopping containers
- introducing API latency
- disconnecting databases
- sending invalid telemetry
- edge node disconnects
- failed authentication attempts

This will demonstrate real monitoring and observability capabilities.

---

# 10. Logging and Debugging Strategy

The system will include structured logging to assist testing and debugging.

## Planned Logging Areas

- authentication events
- telemetry events
- service failures
- container status
- API requests
- alert generation

Logs will support:

- debugging
- testing evidence
- final report screenshots
- failure analysis

---

# 11. Evidence Collection Strategy

Testing evidence will be collected continuously for academic documentation.

## Evidence Types

- screenshots
- Docker logs
- Postman results
- dashboard outputs
- service registration screenshots
- API responses
- telemetry examples
- alert examples

This evidence will support:

- weekly logs
- interim report
- interim presentation
- final report
- final presentation

---

# 12. MVP Testing Priorities

The MVP phase will prioritise testing of:

- API Gateway
- Eureka registration
- authentication
- monitoring service
- Docker deployment
- React dashboard
- telemetry ingestion
- alert generation

Advanced testing such as Kubernetes validation and AI anomaly testing will remain optional.

---

# 13. Performance and Scalability Testing

Basic performance validation may be performed to evaluate:

- API responsiveness
- telemetry ingestion behaviour
- dashboard responsiveness
- container resource usage

Potential future scalability testing may include:

- concurrent telemetry submissions
- high-frequency monitoring requests
- multi-device telemetry simulation
- container stress testing

---

# 14. Future Testing Extensions

Possible future improvements include:

- automated CI/CD testing
- GitHub Actions pipelines
- performance testing
- load testing
- Prometheus integration
- automated UI testing
- distributed stress testing

These features may be added if time permits.

---

# 15. Acceptance Validation Strategy

The platform will be considered operationally successful when the following capabilities function correctly:

- services register with Eureka
- API Gateway routes requests successfully
- JWT authentication works correctly
- telemetry is received and stored
- alerts are generated during failures
- dashboard visualises monitoring data
- Docker Compose deployment operates reliably
- edge telemetry communication functions correctly

These validation goals align with the MVP objectives and placement deliverables.

---

# 16. Conclusion

Testing is a critical component of EdgeCloud Monitor due to the distributed and cloud-native nature of the system.

The project will use a structured multi-level testing strategy combining:

- unit testing
- integration testing
- deployment testing
- observability validation
- telemetry validation
- real-world infrastructure testing

to ensure reliability, stability, and maintainability throughout development.

The testing strategy also supports strong academic documentation and engineering evidence for placement deliverables.