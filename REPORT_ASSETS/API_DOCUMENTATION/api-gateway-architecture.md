# API Gateway Architecture and Routing Configuration

## Purpose

The API Gateway acts as the single entry point for all external requests entering the EdgeCloud Monitor platform.

Its responsibilities include:

- Centralised request routing
- Service discovery integration
- Security enforcement
- Route management
- Error handling
- Future JWT validation

The gateway simplifies communication between clients and backend microservices while reducing direct service exposure.

---

## Route Mapping Configuration

| Route Pattern | Target Service |
|---------------|---------------|
| /api/v1/auth/** | Authentication Service |
| /api/v1/monitoring/** | Monitoring Service |
| /api/v1/devices/** | Device Service |
| /api/v1/alerts/** | Alert Service |

---

## API Gateway Request Flow

Client Request

↓

API Gateway

↓

Eureka Service Discovery

↓

Target Microservice

Examples:

- /api/v1/auth/** → Authentication Service
- /api/v1/monitoring/** → Monitoring Service
- /api/v1/devices/** → Device Service
- /api/v1/alerts/** → Alert Service

---

## Eureka Service Discovery Integration

The API Gateway uses Eureka for dynamic service discovery.

Services register themselves with Eureka during startup.

The gateway routes requests using logical service names rather than fixed IP addresses.

Examples:

- lb://EDGECLOUD-AUTH-SERVICE
- lb://EDGECLOUD-MONITORING-SERVICE
- lb://EDGECLOUD-DEVICE-SERVICE
- lb://EDGECLOUD-ALERT-SERVICE

Benefits:

- Dynamic routing
- Improved scalability
- Reduced configuration overhead
- Simplified deployment

---

## Security Responsibilities

The API Gateway provides the first layer of request security.

### Public Routes

- POST /api/v1/auth/login
- POST /api/v1/auth/register
- GET /actuator/health
- GET /actuator/info

### Protected Routes

- /api/v1/monitoring/**
- /api/v1/devices/**
- /api/v1/alerts/**

### JWT Responsibilities

The gateway has been prepared for JWT authentication filtering.

Expected token format:

Authorization: Bearer <token>

Future validation will be integrated with the Authentication Service.

---

## Error Handling Behaviour

The gateway supports predictable error responses.

### Common Responses

| Status Code | Description |
|-------------|-------------|
| 401 | Unauthorised |
| 403 | Forbidden |
| 404 | Route Not Found |
| 500 | Internal Gateway Error |
| 503 | Service Unavailable |

### Example Failure Scenarios

- Invalid route
- Missing JWT token
- Invalid JWT token
- Backend service unavailable
- Service discovery failure
- Connection refused

---

## Testing Evidence

Gateway routing validation was completed through Postman testing.

Validated routes:

- Authentication Service
- Monitoring Service
- Device Service
- Alert Service
- Invalid Route Handling

Evidence location:

REPORT_ASSETS/API_DOCUMENTATION/gateway-route-testing.md

Associated screenshots:

- auth-route.png
- monitoring-route.png
- device-route.png
- alert-route.png
- invalid-route.png
- gateway-health.png

---

## Deployment Overview

The API Gateway is deployed as part of the Docker Compose environment.

The gateway communicates with:

- Eureka Discovery Service
- Authentication Service
- Monitoring Service
- Device Service
- Alert Service

All service communication occurs through the Docker network and Eureka service discovery.

---

## Conclusion

The API Gateway provides centralised routing, service discovery integration, security preparation, and error handling for the EdgeCloud Monitor platform. Gateway routing behaviour has been validated and documented to support future development, testing, deployment, and reporting activities.