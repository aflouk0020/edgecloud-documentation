# WEEK 03 PROGRESS REPORT  
## EdgeCloud Monitor – Sprint 2 Monitoring Service Implementation
### Overview
During Week 03, development moved from the Sprint 1 infrastructure foundation into Sprint 2 Monitoring and Device work.
The main focus of this week was the implementation and validation of the Monitoring Service. This included service registration, health monitoring, telemetry ingestion, historical metrics retrieval, database persistence, Docker validation, Eureka registration, and API Gateway route verification.
This work established the core observability layer required for EdgeCloud Monitor.
---
# Objectives Completed
- Created Monitoring Service package structure
- Configured Monitoring Service dependencies
- Connected Monitoring Service to `monitoring_db`
- Registered Monitoring Service with Eureka
- Implemented monitored service registration
- Implemented service health checks
- Implemented response latency measurement
- Persisted service metrics
- Implemented telemetry ingestion
- Persisted edge telemetry metrics
- Implemented historical metrics retrieval
- Validated API Gateway routing
- Tested Monitoring Service APIs
- Verified database records
- Collected Docker, Eureka, API, and database evidence
- Documented Monitoring Service design and metrics workflow
---
# Monitoring Service Implementation
## Technologies Used
- Java 21
- Spring Boot 3.5.x
- Spring Data JPA
- Spring Boot Actuator
- Spring Cloud Netflix Eureka Client
- MySQL
- Docker Compose
- API Gateway
- Maven
- GitHub
## Completed Components
The Monitoring Service now includes:
- controller layer
- service layer
- repository layer
- entity layer
- DTO layer
- validation support
- exception handling
- database persistence
- Eureka client registration
- actuator health endpoint
---
# Service Registration Workflow
A monitored service registration API was implemented to allow backend services to be registered for monitoring.
Endpoint:
```text
POST /api/v1/monitoring/services

Example payload:

{
  "serviceName": "device-service",
  "serviceUrl": "http://device-service:8083"
}

Implemented behaviour:

* valid service registration
* duplicate service detection
* request validation
* monitored service persistence
* service status storage

Database table:

monitored_services

⸻

Health Monitoring Workflow

A health check workflow was implemented to evaluate registered services.

Endpoint:

POST /api/v1/monitoring/health-checks

The workflow:

1. Loads registered services from monitoring_db
2. Calls the target service health endpoint
3. Measures response latency
4. Records status as UP or DOWN
5. Stores monitoring results in service_metrics
6. Updates the current service status

Stored metrics include:

* service ID
* response time in milliseconds
* HTTP status code
* uptime status
* recorded timestamp

⸻

Telemetry Ingestion Workflow

A telemetry ingestion API was implemented for Raspberry Pi devices and simulated edge agents.

Endpoint:

POST /api/v1/monitoring/telemetry

Example payload:

{
  "deviceId": "pi-node-01",
  "cpuUsage": 45.5,
  "memoryUsage": 60.2,
  "temperature": 51.4
}

Implemented behaviour:

* telemetry request validation
* CPU usage storage
* memory usage storage
* temperature storage
* device ID storage
* heartbeat status assignment
* timestamp generation

Database table:

telemetry_metrics

⸻

Historical Metrics API

A historical metrics endpoint was implemented to support dashboard visualisation and future analytics.

Endpoint:

GET /api/v1/monitoring/history

The response includes:

* service health history
* response latency history
* telemetry history
* CPU usage
* memory usage
* temperature
* heartbeat status
* recorded timestamps

Results are ordered by recorded timestamp using newest-first ordering.

⸻

Docker and Eureka Validation

The Monitoring Service was tested inside the Docker Compose environment.

Validated containers included:

Component	Status
Discovery Service	Healthy
API Gateway	Healthy
Authentication Service	Healthy
Monitoring Service	Healthy
Device Service	Healthy
Alert Service	Healthy
MySQL databases	Healthy

The Eureka dashboard confirmed that all core backend services registered successfully:

EDGECLOUD-API-GATEWAY
EDGECLOUD-AUTH-SERVICE
EDGECLOUD-MONITORING-SERVICE
EDGECLOUD-DEVICE-SERVICE
EDGECLOUD-ALERT-SERVICE

⸻

API Gateway Route Validation

Monitoring routes were tested through the API Gateway using:

/api/v1/monitoring/**

Gateway route validation confirmed that requests reached the gateway and were intercepted by the security layer when no JWT token was provided.

This confirmed that the Monitoring Service route was active and protected.

⸻

Database Validation

The following tables were validated in monitoring_db:

monitored_services
service_metrics
telemetry_metrics

Database checks confirmed:

* registered services were persisted
* service status updates were stored
* health check metrics were saved
* latency values were recorded
* telemetry metrics were stored
* timestamps were generated correctly

⸻

API Testing Completed

The following workflows were manually tested:

* valid service registration
* duplicate service registration
* invalid service registration
* health check execution
* telemetry ingestion
* invalid telemetry payload
* historical metrics retrieval
* gateway route validation
* database persistence verification

⸻

Technical Challenges Encountered

Java Version Conflict

Some Maven commands initially failed because the terminal session was using Java 11 instead of Java 21.

Resolution:

JAVA_HOME was updated to Java 21 before running Maven.

⸻

Docker Environment Variables

Docker Compose initially used random host ports when the .env file was not loaded.

Resolution:

docker compose --env-file ../env/.env up -d

This restored expected ports:

Eureka: 8761
API Gateway: 8095
Monitoring Service: 8082

⸻

Docker Image Rebuild

A 404 error occurred because Docker was running an older Monitoring Service image.

Resolution:

The Monitoring Service image was rebuilt using Docker Compose.

⸻

Evidence Collected

Evidence collected during Week 03 includes:

* Docker container health screenshots
* Eureka service registration screenshots
* service registration API responses
* duplicate request responses
* validation error responses
* health check responses
* telemetry ingestion responses
* historical metrics responses
* MySQL database table records
* API Gateway route validation responses
* GitHub Pull Request screenshots

⸻

Current Platform Status

Component	Status
Discovery Service	Operational
API Gateway	Operational
Authentication Service	Operational
Monitoring Service	Operational
Monitoring Database	Operational
Service Registration	Implemented
Health Monitoring	Implemented
Telemetry Ingestion	Implemented
Historical Metrics API	Implemented
Docker Compose Validation	Completed

⸻

Next Planned Activities

Upcoming work will focus on:

* Device Service implementation
* device registration workflows
* heartbeat tracking
* device status management
* edge telemetry agent integration
* React dashboard connection to monitoring APIs
* Alert Service rule integration

⸻

Conclusion

Week 03 successfully transitioned the project from infrastructure setup into functional observability development.

The Monitoring Service now provides the core monitoring capabilities required by EdgeCloud Monitor, including service registration, health checks, response latency tracking, telemetry ingestion, database persistence, and historical metrics retrieval.

This establishes a strong foundation for dashboard visualisation, edge device monitoring, and future alert generation.