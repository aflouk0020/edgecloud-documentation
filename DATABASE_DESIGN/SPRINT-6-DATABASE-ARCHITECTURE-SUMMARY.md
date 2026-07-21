# Sprint 6 Database Architecture Summary

## 1. Overview

Sprint 6 continued to validate the database architecture supporting the EdgeCloud Monitor cloud-native platform.

The database design follows the microservice database ownership principle, where each service maintains responsibility for its own data storage and exposes information through REST APIs.

---

# 2. Database Architecture

The platform uses independent databases aligned with individual microservices.

Architecture:

Authentication Service

↓

auth_db


Monitoring Service

↓

monitoring_db


Device Service

↓

device_db


Alert Service

↓

alert_db

---

# 3. Monitoring Database

The Monitoring Service database stores operational monitoring information.

Responsibilities:

- Monitored service information.
- Health check results.
- Response time metrics.
- Telemetry measurements.
- Historical monitoring records.

The database supports analytics and operational visibility.

---

# 4. Device Database

The Device Service database manages edge device information.

Responsibilities:

- Device registration.
- Device metadata.
- Device status.
- Heartbeat information.

This supports Raspberry Pi and simulated edge device workflows.

---

# 5. Alert Database

The Alert Service database manages operational incidents.

Responsibilities:

- Alert records.
- Alert severity.
- Alert status.
- Resolution information.
- Incident workflow data.

---

# 6. Database Validation Results

Sprint 6 validation confirmed:

- Services maintained independent database ownership.
- Data communication occurred through APIs.
- No direct database sharing existed between services.
- Telemetry and alert records were stored successfully.
- Monitoring workflows operated correctly.

---

# 7. Database Architecture Outcome

The database architecture continues to support cloud-native principles:

- Service independence.
- Database isolation.
- API-driven communication.
- Scalable microservice design.
- Clear ownership boundaries.

---

# 8. Future Work

(To be defined after project review)
