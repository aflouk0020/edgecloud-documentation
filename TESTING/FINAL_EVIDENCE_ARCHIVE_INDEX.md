# Final Testing Evidence Archive Index

## 1. Overview

This document provides an organised index of the final testing evidence collected during the development of EdgeCloud Monitor.

The purpose of this archive is to ensure that technical validation evidence is structured and accessible for final project reporting, assessment review, and future maintenance.

---

# 2. Testing Evidence Categories

## End-to-End Validation Evidence

Location:

TESTING/

Includes:

- Sprint 9 Device Inventory Dashboard automated and runtime evidence
- Sprint 9 Device Registration and Lifecycle automated, runtime, security, and manual-capture evidence
- SCRUM-714 Sprint 8 integrated validation evidence
- SCRUM-713 Alert Suppression and Maintenance evidence
- SCRUM-712 Alert Escalation Policy Engine evidence

- SCRUM-64 End-to-End Validation
- Complete platform workflow validation
- Service communication verification
- Deployment verification

---

## Edge Device Testing Evidence

Location:

TESTING/

Includes:

- SCRUM-66 Raspberry Pi compatibility validation
- SCRUM-67 simulated telemetry validation

Evidence covers:

- Edge telemetry collection
- Device communication
- Monitoring data submission

---

## Docker and Deployment Evidence

Location:

DEPLOYMENT/

Includes:

- Docker Compose integration validation
- Container startup verification
- Service networking validation
- Environment configuration validation

---

## API Testing Evidence

Location:

API_DOCUMENTATION/

Includes:

- API specifications
- REST communication documentation
- Service integration validation

Validated areas:

- Authentication APIs
- Monitoring APIs
- Device APIs
- Alert APIs

---

## Performance Testing Evidence

Location:

TESTING/SCRUM-103-PERFORMANCE-LOAD-TESTING.md

Includes:

- Monitoring API load observation
- Telemetry submission testing
- Response time observations
- Operational performance validation

---

## Metric Aggregation Evidence

Location:

TESTING/SCRUM-695-METRIC-AGGREGATION-EVIDENCE.md

Includes:

- service aggregation validation
- device aggregation validation
- date-range validation
- empty-result handling
- project aggregation 501 limitation evidence

---

## Project Observability Workspace Evidence

Location:

TESTING/SCRUM-692-PROJECT-OBSERVABILITY-WORKSPACE-EVIDENCE.md

Includes:

- workspace summary endpoint validation
- project authorisation evidence
- project-centred dashboard route validation
- service and device enrichment safety evidence
- empty, loading, error, unauthorised, archived, and partial-success states
- dependency note for future project-scoped observability aggregation

---

## Service Health Overview Evidence

Location:

TESTING/SCRUM-696-SERVICE-HEALTH-OVERVIEW-EVIDENCE.md

Includes:

- public service-health endpoint validation
- internal Monitoring Service service-health query contract
- project isolation flow
- health mapping rules
- summary counts and deterministic service sorting
- manual and automatic refresh validation
- responsive table/card UI evidence
- backend and frontend final validation evidence

---

## Edge Device Health Overview Evidence

Location:

TESTING/SCRUM-697-EDGE-DEVICE-HEALTH-OVERVIEW-EVIDENCE.md

Includes:

- public device-health endpoint validation
- internal Device Service device-health query contract
- internal Monitoring Service telemetry-freshness contract
- project isolation flow
- device-health mapping rules
- deterministic device sorting
- manual and automatic refresh validation
- responsive table/card UI evidence
- backend and frontend final validation evidence

---

## Historical Metrics Explorer Evidence

Location:

TESTING/SCRUM-694-HISTORICAL-METRICS-EVIDENCE.md

Includes:

- project historical-metrics endpoint validation
- internal Monitoring Service historical query contract
- project isolation flow
- date-range and pagination validation
- deterministic ordering evidence
- PARTIAL / UNAVAILABLE / NO_DATA behaviour
- basic timeline/list UI validation
- final build and test evidence

---

## Real-Time Observability Updates Evidence

Location:

TESTING/SCRUM-698-REAL-TIME-OBSERVABILITY-UPDATES-EVIDENCE.md

Includes:

- shared polling foundation
- summary, service-health, device-health, and historical polling behaviour
- connection states and non-intrusive warnings
- hidden-tab pause and visibility recovery
- retry/backoff and cleanup validation
- final dashboard test and build evidence

## Alert Rule Management Evidence

Location:

TESTING/SCRUM-701-ALERT-RULE-MANAGEMENT-EVIDENCE.md

Includes:

- project-scoped AlertRule model and Flyway migration
- secured REST endpoint contract
- JWT and project-role authorization
- device/service association validation
- API Gateway routing
- responsive dashboard rule-management UI
- 28 passing Alert Service tests and 125 passing dashboard tests
- successful Java 21 compile/package and dashboard production build
- manual screenshot evidence marked pending

---

## Alert Rule Evaluation Engine Evidence

Location:

TESTING/SCRUM-702-ALERT-RULE-EVALUATION-ENGINE-EVIDENCE.md

Includes:

- active device and service ownership resolution
- persisted monitoring sample to internal rule-evaluation flow
- project, metric, device, and service scope enforcement
- BigDecimal threshold comparison for all supported operators
- stable sample identifiers and duplicate-processing protection
- downstream failure isolation and bearer-token propagation
- selective candidate lookup, deterministic ordering, and controlled 500-rule `< 1,000 ms` performance evidence
- Java 21 validation across Project, Alert, and Monitoring services
- manual screenshots and runtime captures marked pending

---

## Alert Event Generation and Lifecycle Evidence

Location:

TESTING/SCRUM-703-ALERT-EVENT-GENERATION-LIFECYCLE-EVIDENCE.md

Includes:

- durable OPEN and RESOLVED alert-event lifecycle
- AlertEvaluationResult orchestration and evidence snapshots
- MySQL generated-column active uniqueness design
- real MySQL 8.4 Testcontainers and 20-way concurrency proof
- resolution, re-trigger, and multiple-resolved-history evidence
- project-scoped V2 list/detail API, isolation, filters, and pagination
- controlled lifecycle/query performance measurements
- API Gateway routing and JWT protection
- responsive project Alert History dashboard and full frontend validation
- all 15 acceptance criteria marked with concrete evidence
- manual screenshots and runtime captures marked pending

---

## Historical Metrics CSV Export Evidence

Location:

TESTING/SCRUM-699-EXPORT-PROJECT-OBSERVABILITY-METRICS-EVIDENCE.md

Includes:

- project-scoped CSV export validation
- public Project Service export endpoint
- historical query and bounded CSV generation flow
- project isolation and security rules
- CSV structure and filename handling
- frontend export button and download behaviour
- manual and automatic evidence capture checklist
- backend and frontend final validation evidence

---

# 3. Platform Validation Coverage

The final evidence collection demonstrates validation of:

- Microservice communication
- API gateway routing
- Database separation
- Docker deployment
- Edge telemetry workflows
- Monitoring functionality
- Alert workflows
- Dashboard integration

---

# 4. Report Asset Organisation

Supporting assets are organised within:

REPORT_ASSETS/

and include:

- Screenshots
- Testing outputs
- Deployment evidence
- Presentation materials

---

# 5. Evidence Management Outcome

The evidence archive provides a structured reference for:

- Final MSc report preparation
- Presentation preparation
- Demonstration workflow
- Future project continuation
