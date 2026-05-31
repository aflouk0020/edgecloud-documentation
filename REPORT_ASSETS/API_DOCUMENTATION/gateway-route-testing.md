# API Gateway Route Testing

## Objective

Validate API Gateway route forwarding, service discovery integration, and error handling behaviour using Postman.

## Environment

- Docker Compose deployment
- Eureka Discovery Server
- API Gateway
- Authentication Service
- Monitoring Service
- Device Service
- Alert Service

Gateway URL:

http://localhost:8095

---

## Route Validation Results

### Authentication Service

Request:

GET /api/v1/auth/...

Result:

- Request forwarded successfully
- Expected response received

Status: PASS

---

### Monitoring Service

Request:

GET /api/v1/monitoring/...

Result:

- Request forwarded successfully
- Service reachable through Eureka routing

Status: PASS

---

### Device Service

Request:

GET /api/v1/devices/...

Result:

- Request forwarded successfully

Status: PASS

---

### Alert Service

Request:

GET /api/v1/alerts/...

Result:

- Request forwarded successfully

Status: PASS

---

### Invalid Route Test

Request:

GET /api/v1/does-not-exist

Response:

404 Not Found

Status: PASS

---

## Gateway Error Handling Validation

Scenario:

Monitoring service stopped.

Request:

GET /api/v1/monitoring/actuator/health

Response:

500 Internal Server Error

Expected gateway failure behaviour observed.

Status: PASS

---

## Evidence

Screenshots saved under:

REPORT_ASSETS/SCREENSHOTS/API_GATEWAY/

- gateway-health.png
- auth-route-test.png
- monitoring-route-test.png
- device-route-test.png
- alert-route-test.png
- invalid-route-test.png

---

## Conclusion

API Gateway routing was successfully validated.

Verified:

- Route forwarding
- Eureka service discovery integration
- Docker networking
- Invalid route handling
- Backend service failure behaviour
- Gateway logging