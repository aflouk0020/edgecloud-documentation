# Sprint 6 Completion Report

## 1. Sprint Overview

Sprint 6 focused on improving the observability, stability, and operational readiness of the EdgeCloud Monitor platform.

The sprint moved the platform beyond basic monitoring functionality by introducing analytics capabilities, configurable monitoring thresholds, alert workflow preparation, infrastructure validation, and performance observation testing.

The main objective was to ensure that the cloud-native monitoring platform could reliably collect system information, process operational events, and provide meaningful visibility into distributed services and edge devices.

---

# 2. Sprint Objectives

The objectives of Sprint 6 were:

- Improve monitoring visibility through analytics and metrics summaries.
- Introduce configurable monitoring behaviour through externalised thresholds.
- Validate alert generation and notification preparation workflows.
- Review Docker Compose infrastructure stability.
- Perform lightweight performance and load observation testing.
- Improve evidence collection for final reporting.

---

# 3. Completed User Stories

## SCRUM-97 Monitoring Analytics Summary Metrics

This story introduced monitoring analytics capabilities to provide higher-level visibility of system performance.

The implementation focused on transforming collected monitoring data into meaningful operational summaries.

Key outcomes:

- Monitoring metrics aggregation.
- Service health visibility.
- Historical monitoring information.
- Analytics-ready data structures.

This provides the foundation required for dashboard visualisation and future operational reporting.

---

## SCRUM-98 Configurable Monitoring Thresholds

This story introduced configurable monitoring thresholds to avoid hard-coded monitoring behaviour.

The platform now supports configurable values for:

- High latency detection.
- Device offline detection intervals.

The configuration approach improves maintainability because monitoring behaviour can be adjusted without changing application logic.

---

## SCRUM-100 Notification Preparation Workflow

This story documented the preparation of notification workflows connected to monitoring events.

The workflow establishes the foundation for future alert delivery mechanisms by defining:

- Alert event generation.
- Notification preparation.
- Event-driven communication flow.

The implementation keeps notification responsibilities separated from monitoring responsibilities following microservices principles.

---

## SCRUM-101 Docker Compose Infrastructure Optimisation

This story reviewed and improved the Docker Compose deployment environment.

Validation included:

- Service startup reliability.
- Container communication.
- Database connectivity.
- Environment configuration consistency.

The review confirmed that the distributed environment remained stable as additional services were introduced.

---

## SCRUM-103 Performance and Load Observation Testing

This story introduced lightweight performance testing scripts to evaluate API responsiveness.

Testing covered:

- Monitoring API requests.
- Telemetry submission requests.
- Alert workflow activity.
- Docker resource observation.

Results demonstrated successful request handling with no failed requests during testing.

---

# 4. Technical Achievements

## Monitoring Service

The Monitoring Service was enhanced with:

- Service health monitoring.
- Historical metrics retrieval.
- Analytics summaries.
- Telemetry processing support.

The service continues to act as the central observability component of the platform.

---

## Alert Service

The Alert Service workflow was validated through:

- Alert creation.
- Severity handling.
- Root cause suggestion generation.
- Active alert management.

The architecture maintains separation between monitoring detection and alert management.

---

## Infrastructure Stability

The Docker Compose environment was reviewed to ensure:

- Correct service networking.
- Database container availability.
- Environment variable configuration.
- Reliable multi-container startup.

---

## Performance Validation

Performance observation testing produced the following results:

Monitoring API:

- Requests: 100
- Successful requests: 100
- Failed requests: 0
- Average response time: 9.71 ms

Telemetry Submission API:

- Requests: 100
- Successful requests: 100
- Failed requests: 0
- Average response time: 9.44 ms

These results demonstrate stable API behaviour under lightweight load conditions.

---

# 5. Testing Evidence

Evidence collected during Sprint 6 includes:

- Monitoring analytics validation.
- Docker Compose validation.
- Performance load testing results.
- API response verification.
- Alert workflow testing.
- Container resource observations.

---

# 6. Challenges and Solutions

## Challenge: Increasing system complexity

As additional services were introduced, maintaining reliable communication became more challenging.

Solution:

The project continued using clear microservice boundaries, Docker networking, and independent service responsibilities.

---

## Challenge: Maintaining configurable monitoring behaviour

Hard-coded monitoring rules reduce maintainability.

Solution:

External configuration values were introduced to allow operational thresholds to be adjusted independently.

---

# 7. Sprint Outcome

Sprint 6 successfully improved the operational maturity of EdgeCloud Monitor.

The platform now provides:

- Improved monitoring visibility.
- Configurable monitoring behaviour.
- Alert workflow foundations.
- Validated Docker deployment stability.
- Performance evidence for reporting.

The sprint established a stronger foundation for future dashboard improvements and advanced observability features.

---

# 8. Future Work

(To be defined after sprint review)

