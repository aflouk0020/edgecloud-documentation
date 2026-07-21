# SCRUM-64 End-to-End Edge Telemetry Validation
## Purpose
This document records the end-to-end validation of the EdgeCloud Monitor edge telemetry workflow.
The validation confirms that telemetry and heartbeat data can travel from the Python Edge Telemetry Agent through the API Gateway to the backend services and databases.
## Validated Flow
### Telemetry Flow
Edge Telemetry Agent → API Gateway → Monitoring Service → monitoring_db
### Heartbeat Flow
Edge Telemetry Agent → API Gateway → Device Service → device_db
## Validation Summary
The validation confirmed that the Edge Telemetry Agent can run successfully, generate simulated edge metrics, submit telemetry payloads, send heartbeat messages, and support backend persistence through the Monitoring Service and Device Service.
## Infrastructure Validation
During testing, the API Gateway Docker port mapping was corrected.
The gateway application was running internally on port 8095, but Docker Compose was originally forwarding the host port to container port 8080.
The Docker Compose mapping was corrected from:
```text
${GATEWAY_PORT}:8080

to:

${GATEWAY_PORT}:8095

The health check was also corrected from:

http://localhost:8080/actuator/health

to:

http://localhost:8095/actuator/health

After recreation, the API Gateway container reported:

0.0.0.0:8095->8095/tcp

The Gateway health endpoint returned HTTP 200 with status UP.

Authentication Validation

The Auth Service database initially contained no users.

A test administrator account was created through the API Gateway:

POST /api/v1/auth/register

A successful login was then completed through:

POST /api/v1/auth/login

The login returned a JWT token, which was used to authenticate API Gateway requests to protected monitoring and device endpoints.

Telemetry Validation

A JWT-authenticated telemetry request was sent through the API Gateway:

POST /api/v1/monitoring/telemetry

The request returned:

HTTP/1.1 201

The response confirmed that the Monitoring Service accepted and persisted the telemetry record.

Example telemetry fields validated:

deviceId
cpuUsage
memoryUsage
temperature
heartbeatStatus
recordedAt

Heartbeat Validation

A JWT-authenticated heartbeat request was sent through the API Gateway:

POST /api/v1/devices/heartbeat

The request returned:

HTTP/1.1 200

The response confirmed that the Device Service updated the registered device status and last heartbeat timestamp.

Validated device state:

deviceName: heartbeat-pi-01
status: ONLINE
lastHeartbeat: updated successfully

Database Persistence Validation

monitoring_db

The telemetry_metrics table contained telemetry records submitted by the Edge Telemetry Agent and through the API Gateway.

The validated records included:

device_id
cpu_usage
memory_usage
temperature
heartbeat_status
recorded_at

device_db

The edge_devices table confirmed that the registered device was updated correctly.

The validated fields included:

id
device_name
status
last_heartbeat

The tested device was updated to:

heartbeat-pi-01
ONLINE

Failure Behaviour Validation

Failure behaviour was also observed.

When telemetry and heartbeat requests were sent through the API Gateway without an Authorization header, the Gateway returned:

HTTP 401 Unauthorized
Missing or invalid Authorization header

The Python Edge Telemetry Agent logged the failure clearly and continued running without crashing.

This confirms that backend failure or rejected requests are handled safely by the agent.

Evidence Collected

Evidence collected during validation included:

* Docker container status output
* API Gateway health endpoint response
* API Gateway route configuration
* Auth Service registration response
* Auth Service login response
* JWT-authenticated telemetry response
* JWT-authenticated heartbeat response
* Monitoring database telemetry records
* Device database heartbeat and status records
* Python Edge Telemetry Agent runtime logs
* Failure handling logs showing HTTP 401 responses

Conclusion

The end-to-end edge telemetry validation was successful.

The platform successfully demonstrated telemetry and heartbeat communication across:

Python Edge Telemetry Agent
API Gateway
Monitoring Service
Device Service
monitoring_db
device_db

This validates the core edge-to-cloud monitoring workflow required for EdgeCloud Monitor and provides strong evidence for Sprint 2 completion, interim reporting, and future dashboard integration.

