# Sprint 6 Observability Architecture Summary

## 1. Overview

Sprint 6 improved the observability capabilities of the EdgeCloud Monitor platform by strengthening the relationship between monitoring, telemetry collection, analytics, and alert management.

The architecture follows cloud-native principles by keeping responsibilities separated between independent microservices while allowing operational data to flow through defined REST API communication paths.

---

# 2. Observability Workflow

The monitoring workflow follows this sequence:

User

↓

React Dashboard

↓

API Gateway

↓

Monitoring Service

↓

Monitoring Data Processing

↓

Alert Service

↓

Alert Management


The dashboard provides visibility while backend services remain responsible for data collection, processing, and operational decisions.

---

# 3. Monitoring Service Responsibilities

The Monitoring Service acts as the central observability component.

Responsibilities include:

- Registering monitored services.
- Performing health checks.
- Collecting service availability information.
- Receiving edge telemetry.
- Storing monitoring metrics.
- Providing analytics information.

Key capabilities introduced during Sprint 6:

- Historical metrics retrieval.
- Service availability tracking.
- Monitoring analytics summaries.
- Performance observation support.

---

# 4. Device Telemetry Workflow

Edge devices communicate with the platform through telemetry submission.

Workflow:

Raspberry Pi / Edge Agent

↓

Telemetry REST API

↓

Monitoring Service

↓

Telemetry Storage

↓

Dashboard Visualisation


Collected information includes:

- CPU usage.
- Memory usage.
- Temperature.
- Device heartbeat status.

This provides the foundation for monitoring distributed edge environments.

---

# 5. Alert Architecture

The Alert Service operates independently from monitoring data collection.

Workflow:

Monitoring Event

↓

Alert Creation

↓

Severity Classification

↓

Root Cause Suggestion

↓

Alert Management


The separation allows the platform to scale monitoring and alert processing independently.

---

# 6. Sprint 6 Architecture Improvements

The main architecture improvements delivered during Sprint 6 include:

## Configurable Monitoring Behaviour

Monitoring thresholds were externalised to configuration values.

Examples:

- High latency threshold.
- Device offline detection interval.

This improves maintainability and allows operational changes without modifying application code.

---

## Analytics Layer Preparation

Monitoring analytics capabilities were introduced to transform raw metrics into meaningful operational information.

This supports:

- Dashboard summaries.
- Service health visibility.
- Future reporting capabilities.

---

## Infrastructure Validation

The Docker Compose environment was reviewed to ensure:

- Reliable service startup.
- Stable container communication.
- Correct database connectivity.
- Consistent environment configuration.

---

# 7. Microservice Communication Model

The platform maintains clear service boundaries:

## Monitoring Service

Responsible for:

- Metrics.
- Telemetry.
- Service health.

## Device Service

Responsible for:

- Device registration.
- Device state.
- Heartbeat information.

## Alert Service

Responsible for:

- Alert creation.
- Alert status.
- Incident workflow preparation.

## API Gateway

Responsible for:

- Centralised routing.
- Client communication entry point.

---

# 8. Architecture Outcome

Sprint 6 improved the operational maturity of EdgeCloud Monitor by introducing stronger observability workflows.

The platform now provides a structured foundation for:

- Monitoring distributed services.
- Tracking edge device health.
- Analysing operational metrics.
- Managing system alerts.

The architecture remains aligned with cloud-native principles including service independence, API-based communication, and scalable microservice design.
