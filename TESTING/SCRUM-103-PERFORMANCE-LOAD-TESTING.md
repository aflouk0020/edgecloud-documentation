# SCRUM-103 Performance and Load Observation Testing

## 1. Overview

SCRUM-103 introduced lightweight performance and load observation testing for the EdgeCloud Monitor platform.

The purpose of this activity was to validate that core monitoring workflows could process repeated API requests successfully and provide measurable response time observations.

The testing focused on:

- Monitoring Service API responsiveness.
- Telemetry ingestion performance.
- Alert workflow behaviour.
- Container resource observation during execution.

The objective was not full-scale benchmarking, but operational validation of the MVP monitoring platform under controlled local conditions.

---

# 2. Test Environment

Testing was performed using the local Docker Compose deployment environment.

Environment:

- Operating System: macOS
- Deployment: Docker Compose
- Backend: Spring Boot microservices
- Database: MySQL containers
- Testing scripts: Python request-based scripts

Validated services:

- Monitoring Service
- Alert Service
- Device Service
- API Gateway
- Supporting database containers

---

# 3. Monitoring API Load Test

## Objective

Validate the responsiveness and stability of the Monitoring Service API when receiving repeated read requests.

## Endpoint Tested
GET http://localhost:8082/services

## Test Configuration

Requests:

100

## Results

Successful requests: 100
Failed requests: 0
Total execution time:
0.97 seconds
Average response time:
9.71 ms

## Observation

The Monitoring Service successfully handled repeated API requests without failures.

The response time indicates stable performance for the expected MVP monitoring workload.

---

# 4. Telemetry Submission Load Test

## Objective

Validate the telemetry ingestion workflow used by edge devices.

## Endpoint Tested

POST http://localhost:8082/telemetry

## Test Configuration

Requests:

100

Telemetry payload:

```json
{
  "deviceId": "load-test-device",
  "cpuUsage": 45.5,
  "memoryUsage": 60.0,
  "temperature": 40.0
}
Results
Successful requests: 100
Failed requests: 0

Total execution time:
0.94 seconds

Average response time:
9.44 ms
Observation
The Monitoring Service successfully accepted and stored repeated telemetry submissions.
The workflow demonstrates that the platform can process simulated edge telemetry reliably.
5. Alert Workflow Validation
The Alert Service workflow was validated by generating multiple test alerts.
Test scenario:
Alert type: SERVICE_DOWN
Severity: HIGH
Source service: load-test-service
Example generated alert:
{
  "alertType": "SERVICE_DOWN",
  "severity": "HIGH",
  "message": "Load test alert",
  "sourceService": "load-test-service"
}
Validation confirmed:
Alert creation.
Severity processing.
Active alert storage.
Root cause suggestion generation.
Example suggestion:
Service may be unavailable or its container may have stopped.
6. Docker Resource Observation
During testing, Docker container resources were observed.
The validation confirmed:
All microservices remained running.
Database containers remained available.
No service crashes occurred during testing.
Network communication remained stable.
Observed services included:
API Gateway
Discovery Service
Authentication Service
Monitoring Service
Device Service
Alert Service
MySQL databases
7. Test Results Summary
Test	Requests	Successful	Failed	Average Response
Monitoring API	100	100	0	9.71 ms
Telemetry Submission API	100	100	0	9.44 ms

8. Conclusion
The SCRUM-103 performance observation testing confirmed that the EdgeCloud Monitor MVP maintained stable behaviour under controlled repeated API requests.
The results provide evidence that the monitoring and telemetry workflows are suitable for the current project scope.
The testing also provides measurable evidence for the final MSc project report regarding API responsiveness and system stability.
