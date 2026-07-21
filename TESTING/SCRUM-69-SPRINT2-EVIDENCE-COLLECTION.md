SCRUM-69 Sprint 2 Evidence Collection

1. Introduction

Purpose

The purpose of this activity was to collect, organise, and preserve technical evidence generated during Sprint 2 development of the EdgeCloud Monitor platform.

Sprint 2 introduced the Monitoring Service, Device Service, Edge Telemetry Agent, Raspberry Pi validation activities, simulated telemetry mode, Docker Compose integration, and end-to-end telemetry workflows.

The objective was to ensure that all technical progress could be demonstrated clearly during supervisor meetings, weekly progress reporting, interim report preparation, final report preparation, and future project maintenance.

⸻

2. Sprint 2 Scope

The evidence collection process covered the following Sprint 2 components:

* Monitoring Service
* Device Service
* Edge Telemetry Agent
* Raspberry Pi Validation
* Simulated Telemetry Mode
* Docker Compose Deployment
* Eureka Service Discovery
* API Gateway Integration
* Database Persistence Validation

⸻

3. Monitoring Service Evidence

Monitoring API Validation

Evidence was collected demonstrating successful Monitoring Service operation.

Validated functionality included:

* Telemetry ingestion
* Telemetry persistence
* Monitoring API processing
* Database storage
* Service availability

Evidence Collected

* API request screenshots
* API response screenshots
* Terminal validation logs
* Database query outputs
* Docker service logs

Validation Result

Telemetry submissions were successfully processed and persisted within monitoring_db.

Acceptance Criterion AC1 was satisfied.

⸻

4. Device Service Evidence

Device API Validation

Evidence was collected demonstrating successful Device Service operation.

Validated functionality included:

* Device registration
* Heartbeat processing
* Device retrieval
* Device status updates
* Offline detection support

Evidence Collected

* API request screenshots
* API response screenshots
* Terminal logs
* Database query outputs
* Docker service logs

Validation Result

Heartbeat submissions successfully updated device status and last heartbeat timestamps within device_db.

Acceptance Criterion AC2 was satisfied.

⸻

5. Edge Telemetry Agent Evidence

Agent Execution Validation

Evidence was collected demonstrating successful operation of the Python Edge Telemetry Agent.

Validated functionality included:

* Agent startup
* Telemetry collection
* Telemetry submission
* Heartbeat submission
* Logging behaviour
* Graceful shutdown

Evidence Collected

Example terminal output:

Starting Edge Telemetry Agent
Telemetry interval: 5 seconds
Collected telemetry payload
Telemetry submitted successfully
Heartbeat submitted successfully

Additional evidence included:

* Raspberry Pi execution logs
* Local execution logs
* Simulated mode execution logs

Validation Result

The Edge Telemetry Agent successfully transmitted telemetry and heartbeat information to backend services.

Acceptance Criterion AC3 was satisfied.

⸻

6. Database Persistence Evidence

monitoring_db Validation

Evidence confirmed telemetry persistence within the Monitoring Service database.

Example query:

SELECT device_id,
       cpu_usage,
       memory_usage,
       temperature,
       heartbeat_status,
       recorded_at
FROM telemetry_metrics;

Validation confirmed:

* Telemetry records stored
* Temperature values stored
* CPU metrics stored
* Memory metrics stored
* ONLINE status stored

device_db Validation

Evidence confirmed heartbeat persistence within the Device Service database.

Example query:

SELECT id,
       device_name,
       status,
       last_heartbeat
FROM edge_devices;

Validation confirmed:

* Device records stored
* Heartbeat timestamps updated
* ONLINE status updates applied

Acceptance Criterion AC4 was satisfied.

⸻

7. Docker Compose Evidence

Container Deployment Validation

Evidence was collected confirming successful Docker deployment of Sprint 2 infrastructure.

Validated containers included:

edgecloud-discovery-service
edgecloud-api-gateway
edgecloud-auth-service
edgecloud-monitoring-service
edgecloud-device-service
edgecloud-auth-mysql
edgecloud-monitoring-mysql
edgecloud-device-mysql

Evidence Collected

* Docker Compose startup logs
* Docker container status screenshots
* Docker health check outputs
* Container connectivity validation

Validation Result

All Sprint 2 services started successfully and remained operational.

⸻

8. Eureka Registration Evidence

Service Discovery Validation

Evidence was collected confirming successful Eureka registration.

Registered services included:

API-GATEWAY
AUTH-SERVICE
MONITORING-SERVICE
DEVICE-SERVICE

Evidence Collected

* Eureka dashboard screenshots
* Eureka service registration screenshots
* Service discovery validation logs

Validation Result

Monitoring Service and Device Service successfully registered with Eureka Discovery.

Acceptance Criterion AC5 was satisfied.

⸻

9. Raspberry Pi Validation Evidence

Physical Device Testing

Evidence was collected from a physical Raspberry Pi device.

Environment details:

Python 3.11.2
Linux Raspberry Pi OS
ARM64 Architecture

Validated functionality included:

* Agent startup
* CPU collection
* Memory collection
* Temperature collection
* Telemetry submission
* Heartbeat submission

Evidence Collected

* Raspberry Pi terminal screenshots
* Telemetry submission logs
* Heartbeat submission logs
* Database verification outputs

Validation Result

The Edge Telemetry Agent operated successfully on Raspberry Pi hardware.

⸻

10. Simulated Telemetry Mode Evidence

Simulated Mode Validation

Evidence was collected confirming successful operation without physical hardware.

Example generated values:

CPU Usage: 30.48%
Memory Usage: 67.61%
Temperature: 74.1°C
CPU Usage: 84.14%
Memory Usage: 64.96%
Temperature: 62.6°C

Evidence Collected

* Simulated mode execution logs
* Telemetry submission logs
* Heartbeat submission logs
* Database persistence verification

Validation Result

Simulated telemetry mode successfully generated realistic monitoring data and integrated with backend services.

⸻

11. Weekly Progress Evidence

Sprint 2 progress was recorded within weekly placement documentation.

Evidence included:

* Sprint completion summaries
* Technical achievements
* Validation activities
* Risk management notes
* Upcoming sprint plans

This evidence supports:

* Supervisor reviews
* Placement monitoring
* Interim report preparation
* Final report preparation

⸻

12. Evidence Storage Locations

Sprint 2 evidence was organised within the documentation repository.

Primary locations include:

Documentation/
│
├── REPORT_ASSETS/
│   ├── DEPLOYMENT_IMAGES/
│   ├── API_DOCUMENTATION/
│   ├── SCRUM-66-RASPBERRY-PI-COMPATIBILITY.md
│   ├── SCRUM-67-SIMULATED-TELEMETRY-MODE.md
│   ├── SCRUM-68-DOCKER-COMPOSE-INTEGRATION.md
│   └── SCRUM-69-SPRINT2-EVIDENCE-COLLECTION.md
│
└── WEEKLY_PROGRESS/

Acceptance Criterion AC6 was satisfied.

⸻

13. Acceptance Criteria Verification

Acceptance Criteria	Status
AC1 Monitoring Evidence Collected	Complete
AC2 Device Evidence Collected	Complete
AC3 Edge Agent Evidence Collected	Complete
AC4 Database Evidence Collected	Complete
AC5 Docker and Eureka Evidence Collected	Complete
AC6 Evidence Folder Updated	Complete

⸻

14. Conclusion

Sprint 2 evidence collection was successfully completed. Technical evidence was gathered for the Monitoring Service, Device Service, Edge Telemetry Agent, Raspberry Pi compatibility testing, simulated telemetry mode, Docker Compose deployment, Eureka registration, API Gateway routing, and database persistence validation. The collected evidence provides strong support for weekly placement reporting, supervisor reviews, interim assessment preparation, final report development, and future project maintenance.