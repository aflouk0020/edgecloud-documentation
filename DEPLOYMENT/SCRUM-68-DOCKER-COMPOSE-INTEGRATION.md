SCRUM-68 Docker Compose Integration for Monitoring Service and Device Service

1. Introduction

Purpose

The purpose of this activity was to integrate the Sprint 2 backend services into the EdgeCloud Monitor Docker Compose infrastructure.

Sprint 2 introduced the Monitoring Service and Device Service, both of which required dedicated database containers, Docker networking configuration, service discovery integration, API Gateway routing, and deployment validation.

The objective was to ensure that all backend services could operate within a distributed containerised environment while maintaining service isolation, database ownership, and cloud-native deployment principles.

⸻

2. Sprint 2 Infrastructure Components

Existing Sprint 1 Components

The following services were already deployed within the Docker Compose environment:

* Discovery Service
* API Gateway
* Authentication Service
* Authentication Database

Sprint 2 Components Added

The following components were integrated during Sprint 2:

* Monitoring Service
* Device Service
* monitoring_db
* device_db

Docker Network

All containers communicate through:

edgecloud-network

This network enables service discovery, internal communication, and database connectivity between containers.

⸻

3. Monitoring Service Container Integration

Purpose

The Monitoring Service is responsible for:

* Service health monitoring
* Telemetry processing
* Telemetry persistence
* Monitoring metrics storage
* Device telemetry ingestion

Container Validation

The Monitoring Service container was successfully integrated into Docker Compose.

Validation confirmed:

* Container startup successful
* Eureka registration successful
* Database connectivity successful
* Internal network communication successful
* API endpoint availability successful

⸻

4. Device Service Container Integration

Purpose

The Device Service is responsible for:

* Device registration
* Heartbeat processing
* Device status management
* Offline device detection
* Device metadata storage

Container Validation

The Device Service container was successfully integrated into Docker Compose.

Validation confirmed:

* Container startup successful
* Eureka registration successful
* Database connectivity successful
* Internal network communication successful
* API endpoint availability successful

⸻

5. Database Container Integration

monitoring_db

The Monitoring Service owns a dedicated MySQL database container.

Responsibilities include:

* Telemetry metrics storage
* Monitoring history storage
* Device telemetry persistence

Validation confirmed:

* Database startup successful
* Container healthy
* Monitoring Service connection successful
* Telemetry persistence successful

device_db

The Device Service owns a dedicated MySQL database container.

Responsibilities include:

* Device registration storage
* Heartbeat tracking
* Device status management

Validation confirmed:

* Database startup successful
* Container healthy
* Device Service connection successful
* Heartbeat persistence successful

⸻

6. Docker Compose Validation

Container Startup Validation

Docker Compose successfully started all required Sprint 2 services.

Verified containers included:

edgecloud-discovery-service
edgecloud-api-gateway
edgecloud-auth-service
edgecloud-monitoring-service
edgecloud-device-service
edgecloud-auth-mysql
edgecloud-monitoring-mysql
edgecloud-device-mysql

Validation confirmed:

* Containers started successfully
* Containers remained healthy
* No critical startup failures occurred

⸻

7. Eureka Service Registration Validation

Objective

Verify that Monitoring Service and Device Service successfully register with Eureka Discovery.

Validation Result

The Eureka dashboard displayed:

API-GATEWAY
AUTH-SERVICE
MONITORING-SERVICE
DEVICE-SERVICE

This confirmed:

* Successful service registration
* Successful service discovery
* Successful internal service visibility

Acceptance Criterion AC4 was satisfied.

⸻

8. API Gateway Routing Validation

Monitoring Service Routing

Telemetry requests were successfully routed through the platform.

Request flow:

Edge Telemetry Agent
        ↓
API Gateway
        ↓
Monitoring Service
        ↓
monitoring_db

Validation confirmed:

* Gateway route operational
* Monitoring Service received requests
* Telemetry stored successfully

Device Service Routing

Heartbeat requests were successfully routed through the platform.

Request flow:

Edge Telemetry Agent
        ↓
API Gateway
        ↓
Device Service
        ↓
device_db

Validation confirmed:

* Gateway route operational
* Device Service received requests
* Device status updated successfully

Acceptance Criterion AC5 was satisfied.

⸻

9. Database Connectivity Validation

Monitoring Database Validation

Telemetry data was successfully persisted.

Example verification query:

SELECT device_id,
       cpu_usage,
       memory_usage,
       temperature,
       heartbeat_status,
       recorded_at
FROM telemetry_metrics;

Results confirmed:

* Telemetry persistence
* Database connectivity
* Monitoring Service functionality

Device Database Validation

Device status information was successfully persisted.

Example verification query:

SELECT id,
       device_name,
       status,
       last_heartbeat
FROM edge_devices;

Results confirmed:

* Device persistence
* Heartbeat updates
* ONLINE status updates

Acceptance Criterion AC6 was satisfied.

⸻

10. Docker Networking Validation

Objective

Verify communication between services and databases.

Validation confirmed:

* Service-to-service communication successful
* Service-to-database communication successful
* Gateway-to-service communication successful
* Discovery-to-service communication successful

No networking issues were identified during validation.

⸻

11. Evidence Collected

The following evidence was collected during validation:

* Docker Compose startup logs
* Docker container health status
* Eureka dashboard screenshots
* API Gateway routing evidence
* Monitoring Service logs
* Device Service logs
* Telemetry submission evidence
* Heartbeat submission evidence
* monitoring_db query results
* device_db query results

⸻

12. Acceptance Criteria Verification

Acceptance Criteria	Status
AC1 Monitoring Service Added to Docker Compose	Complete
AC2 Device Service Added to Docker Compose	Complete
AC3 Database Containers Added	Complete
AC4 Eureka Registration Verified	Complete
AC5 Gateway Routing Verified	Complete
AC6 Database Connectivity Verified	Complete

⸻

13. Conclusion

Sprint 2 Docker Compose integration was successfully completed. The Monitoring Service, Device Service, monitoring_db, and device_db containers were integrated into the EdgeCloud Monitor infrastructure and validated through container startup testing, service discovery verification, API Gateway routing validation, database connectivity testing, and end-to-end telemetry workflows. The platform now supports containerised deployment of all Sprint 2 backend services and provides a stable foundation for future Alert Service integration and continued platform expansion.