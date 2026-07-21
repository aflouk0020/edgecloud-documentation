# EdgeCloud Monitor
## API Specification

---

# 1. Introduction

This document defines the planned API structure for EdgeCloud Monitor.

The platform follows an API-first microservices architecture where all communication occurs through REST APIs routed through a central API Gateway.

The API layer is responsible for:

- frontend communication
- service interaction
- telemetry submission
- monitoring operations
- authentication
- alert management

The specification aims to provide clear service boundaries and standardised communication across the platform.

---

# 2. API Architecture Overview

The system follows the architecture:

```text
React Dashboard
        ↓
API Gateway
        ↓
Microservices
```

All external requests must pass through the API Gateway.

The gateway is responsible for:

- routing
- authentication filtering
- request forwarding
- centralised API access

---

# 3. API Design Principles

The APIs follow these design principles:

- RESTful architecture
- stateless communication
- JSON request/response bodies
- JWT-secured endpoints
- service isolation
- versioned endpoints
- standard HTTP response codes

---

# 4. Planned API Gateway Routes

| Route | Target Service |
|---|---|
| /api/v1/auth/** | Authentication Service |
| /api/v1/monitoring/** | Monitoring Service |
| /api/v1/devices/** | Device Service |
| /api/v1/alerts/** | Alert Service |

---

# 5. Authentication Service APIs

## Base Route

```text
/api/v1/auth
```

---

## 5.1 User Login

### Endpoint

```http
POST /api/v1/auth/login
```

### Purpose

Authenticates a user and generates a JWT token.

### Request Body

```json
{
  "email": "user@example.com",
  "password": "password123"
}
```

### Response

```json
{
  "token": "jwt_token_here",
  "role": "ADMIN"
}
```

---

## 5.2 User Registration

### Endpoint

```http
POST /api/v1/auth/register
```

### Purpose

Registers a new platform user.

### Request Body

```json
{
  "email": "user@example.com",
  "password": "password123",
  "role": "OPERATOR"
}
```

---

## 5.3 Token Validation

### Endpoint

```http
GET /api/v1/auth/validate
```

### Purpose

Validates JWT token integrity.

---

# 6. Monitoring Service APIs

## Base Route

```text
/api/v1/monitoring
```

---

## 6.1 Register Monitored Service

### Endpoint

```http
POST /api/v1/monitoring/services
```

### Purpose

Registers a service for monitoring.

### Request Body

```json
{
  "serviceName": "device-service",
  "serviceUrl": "http://device-service:8083"
}
```

---

## 6.2 Get Service Health

### Endpoint

```http
GET /api/v1/monitoring/services
```

### Purpose

Returns current monitored service status.

### Example Response

```json
[
  {
    "serviceName": "auth-service",
    "status": "UP",
    "responseTime": 45
  }
]
```

---

## 6.3 Submit Telemetry Metrics

### Endpoint

```http
POST /api/v1/monitoring/telemetry
```

### Purpose

Receives telemetry from edge devices.

### Request Body

```json
{
  "deviceId": "pi-node-01",
  "cpuUsage": 45.5,
  "memoryUsage": 60.2,
  "temperature": 51.4
}
```

---

## 6.4 Get Historical Metrics

### Endpoint

```http
GET /api/v1/monitoring/history
```

### Purpose

Returns historical monitoring data.

---

# 7. Device Service APIs

## Base Route

```text
/api/v1/devices
```

---

## 7.1 Register Edge Device

### Endpoint

```http
POST /api/v1/devices/register
```

### Purpose

Registers a new edge device.

### Request Body

```json
{
  "deviceName": "raspberry-pi-01",
  "deviceType": "RaspberryPi",
  "ipAddress": "192.168.1.50"
}
```

---

## 7.2 Device Heartbeat

### Endpoint

```http
POST /api/v1/devices/heartbeat
```

### Purpose

Receives heartbeat signal from edge devices.

### Request Body

```json
{
  "deviceId": "pi-node-01",
  "timestamp": "2026-05-19T12:30:00"
}
```

---

## 7.3 Get Registered Devices

### Endpoint

```http
GET /api/v1/devices
```

### Purpose

Returns all registered edge devices.

---

# 8. Alert Service APIs

## Base Route

```text
/api/v1/alerts
```

---

## 8.1 Create Alert

### Endpoint

```http
POST /api/v1/alerts
```

### Purpose

Creates a new alert event.

### Request Body

```json
{
  "alertType": "SERVICE_DOWN",
  "severity": "HIGH",
  "message": "Monitoring service unavailable"
}
```

---

## 8.2 Get Active Alerts

### Endpoint

```http
GET /api/v1/alerts
```

### Purpose

Returns active system alerts.

---

## 8.3 Resolve Alert

### Endpoint

```http
PUT /api/v1/alerts/{id}/resolve
```

### Purpose

Marks an alert as resolved.

---

# 9. Health Check Endpoints

Each microservice will expose health endpoints for monitoring and container orchestration.

Example endpoints:

```http
GET /actuator/health
GET /actuator/info
```

These endpoints will support:

- Docker health checks
- service monitoring
- uptime verification
- observability
- deployment validation

Spring Boot Actuator will be used for service health monitoring.

---

# 10. HTTP Response Standards

The platform will follow standard HTTP status conventions.

| Code | Meaning |
|---|---|
| 200 | Success |
| 201 | Resource Created |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 500 | Internal Server Error |

---

# 11. API Security

The APIs will use JWT authentication.

Protected endpoints require:

```http
Authorization: Bearer <token>
```

The API Gateway will validate JWT tokens before forwarding requests.

---

# 12. API Communication Format

All APIs will use:

- JSON request bodies
- JSON responses
- UTF-8 encoding
- RESTful conventions

---

# 13. Inter-Service Communication

Services communicate internally through REST APIs.

Examples:

```text
Monitoring Service → Alert Service
Monitoring Service → Device Service
```

No direct database access between services is allowed.

---

# 14. API Versioning Strategy

The platform uses URI-based API versioning.

All production APIs use the:

```text
/api/v1/
```

structure.

This approach improves:

- backward compatibility
- future API evolution
- frontend stability
- maintainability
- scalable service evolution

---

# 15. Future API Extensions

Possible future additions include:

- WebSocket support
- MQTT integration
- GraphQL APIs
- Prometheus exporters
- real-time event streaming
- notification APIs

---

# 16. Engineering Benefits

The API-first architecture supports:

- loose coupling
- service scalability
- frontend independence
- distributed deployment
- modular engineering practices

---

# 17. Conclusion

The proposed API specification provides a structured communication layer for EdgeCloud Monitor.

The APIs support:

- monitoring operations
- telemetry collection
- distributed communication
- secure authentication
- alert management
- edge device integration

while maintaining cloud-native microservice engineering principles.