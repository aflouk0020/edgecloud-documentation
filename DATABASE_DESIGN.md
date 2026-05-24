# EdgeCloud Monitor
## Database Design

---

# 1. Introduction

This document defines the database architecture and data ownership strategy for EdgeCloud Monitor.

The platform follows a database-per-service architecture consistent with cloud-native microservices design principles.

Each microservice owns its own database and manages its own data independently.

This approach improves:

- service isolation
- scalability
- maintainability
- deployment independence
- fault isolation

---

# 2. Database Architecture Strategy

The project will use:

- MySQL relational databases
- database-per-service architecture
- isolated service ownership
- REST-based inter-service communication

Direct database sharing between services will not be allowed.

All communication between services will occur through APIs.

---

# 3. Planned Databases

| Service | Database Name |
|---|---|
| Authentication Service | auth_db |
| Monitoring Service | monitoring_db |
| Device Service | device_db |
| Alert Service | alert_db |

---

# 4. Database Design Principles

The database design follows these principles:

- each service owns its schema
- no cross-service foreign keys
- UUID-based identifiers
- relational modelling where appropriate
- timestamps for auditing and tracking
- scalable entity separation
- API-driven data access

---

# 5. Authentication Service Database

## Database Name

```text
auth_db
```

---

## Purpose

Stores:

- users
- authentication data
- user roles
- JWT-related metadata

---

## Planned Tables

### users

| Field | Type | Description |
|---|---|---|
| id | UUID | Primary key |
| email | VARCHAR | Unique user email |
| password_hash | VARCHAR | Encrypted password |
| role | ENUM | User role |
| created_at | TIMESTAMP | Account creation time |
| updated_at | TIMESTAMP | Last update timestamp |

---

## Planned Roles

```text
ADMIN
OPERATOR
VIEWER
```

---

# 6. Monitoring Service Database

## Database Name

```text
monitoring_db
```

---

## Purpose

Stores:

- service monitoring data
- API metrics
- telemetry metrics
- historical monitoring records

---

## Planned Tables

### monitored_services

| Field | Type | Description |
|---|---|---|
| id | UUID | Primary key |
| service_name | VARCHAR | Registered service |
| service_url | VARCHAR | Service endpoint |
| status | ENUM | Current service status |
| created_at | TIMESTAMP | Registration timestamp |

---

### service_metrics

| Field | Type | Description |
|---|---|---|
| id | UUID | Primary key |
| service_id | UUID | Logical reference |
| response_time_ms | DOUBLE | API latency |
| status_code | INT | HTTP response |
| uptime_status | ENUM | UP / DOWN |
| recorded_at | TIMESTAMP | Metric timestamp |

---

### telemetry_metrics

| Field | Type | Description |
|---|---|---|
| id | UUID | Primary key |
| device_id | UUID | Logical device reference |
| cpu_usage | DOUBLE | CPU percentage |
| memory_usage | DOUBLE | Memory percentage |
| temperature | DOUBLE | Device temperature |
| heartbeat_status | ENUM | ONLINE / OFFLINE |
| recorded_at | TIMESTAMP | Metric timestamp |

---

# 7. Device Service Database

## Database Name

```text
device_db
```

---

## Purpose

Stores:

- edge device information
- device registration
- heartbeat tracking
- device metadata

---

## Planned Tables

### edge_devices

| Field | Type | Description |
|---|---|---|
| id | UUID | Primary key |
| device_name | VARCHAR | Device identifier |
| device_type | VARCHAR | Pi / simulated node |
| ip_address | VARCHAR | Device IP |
| status | ENUM | ONLINE / OFFLINE |
| registered_at | TIMESTAMP | Registration time |
| last_heartbeat | TIMESTAMP | Last heartbeat |

---

# 8. Alert Service Database

## Database Name

```text
alert_db
```

---

## Purpose

Stores:

- alerts
- incidents
- system failures
- diagnostic information

---

## Planned Tables

### alerts

| Field | Type | Description |
|---|---|---|
| id | UUID | Primary key |
| alert_type | ENUM | Failure category |
| severity | ENUM | LOW / MEDIUM / HIGH |
| message | TEXT | Alert message |
| source_service | VARCHAR | Trigger source |
| created_at | TIMESTAMP | Alert timestamp |
| resolved | BOOLEAN | Resolution state |

---

## Planned Alert Types

```text
SERVICE_DOWN
HIGH_LATENCY
DEVICE_OFFLINE
DATABASE_FAILURE
CONTAINER_FAILURE
```

---

# 9. Data Relationships

The system avoids direct cross-service database relationships.

Instead:

- services communicate through APIs
- IDs are shared logically
- service boundaries remain isolated

Example:

```text
Monitoring Service → Device Service
```

through REST APIs rather than database joins.

---

# 10. Data Retention Strategy

Monitoring data may grow rapidly over time.

Planned strategies include:

- historical metric limits
- scheduled cleanup
- optional archiving
- efficient timestamp indexing

Monitoring and telemetry platforms may generate large volumes of time-series-like data.

Because of this, long-term production deployments may later require:

- metric aggregation
- archival strategies
- time-series databases
- retention policies
- scheduled cleanup processes

---

# 11. Indexing Strategy

Indexes will be used to improve query performance for monitoring and telemetry operations.

Planned indexing areas include:

- service_name
- device_id
- recorded_at timestamps
- alert severity
- alert resolution state
- user email addresses

Example indexing goals:

- fast telemetry retrieval
- efficient historical metric queries
- rapid alert filtering
- fast authentication lookups

Time-based indexes are especially important for monitoring workloads because telemetry data may grow rapidly.

---

# 12. Audit and Timestamp Strategy

Most entities will contain timestamp fields to support:

- operational tracking
- monitoring history
- debugging
- deployment analysis
- report evidence generation

Common timestamp fields include:

- created_at
- updated_at
- recorded_at
- last_heartbeat

Timestamps will use UTC where possible to maintain consistency across distributed systems.

---

# 13. Database Migration Strategy

Database schema changes will be managed through controlled migration practices.

Planned approach:

- incremental schema evolution
- version-controlled database changes
- environment consistency
- rollback safety

Spring Boot schema management tools such as Flyway or Liquibase may later be integrated if time allows.

Initially, Hibernate auto-generation may be used during early development before migration tooling is introduced.

---

# 14. Backup and Recovery Considerations

Although the project is development-focused, backup and recovery considerations are important for infrastructure reliability.

Planned considerations include:

- Docker volume persistence
- MySQL dump backups
- telemetry data retention
- database recreation procedures
- container recovery workflows

These considerations improve deployment resilience and operational reliability.

---

# 15. Database Security Considerations

Security measures include:

- password hashing
- JWT authentication
- restricted database access
- isolated service databases
- environment variable configuration
- container isolation

---

# 16. Scalability Considerations

The database design supports future scalability through:

- independent database scaling
- service isolation
- modular schema design
- distributed deployment readiness

---

# 17. Future Database Extensions

Possible future additions include:

- Redis caching
- time-series databases
- analytics storage
- distributed logging
- audit tables
- Prometheus integration

---

# 18. Engineering Benefits

The selected database architecture demonstrates:

- cloud-native engineering principles
- distributed systems thinking
- microservice isolation
- scalable backend architecture
- API-first design

---

# 19. Conclusion

The proposed database design provides a modular and scalable foundation for EdgeCloud Monitor.

The architecture supports:

- distributed monitoring
- telemetry collection
- service isolation
- observability
- cloud-native deployment

while maintaining clean microservice boundaries and professional engineering practices.