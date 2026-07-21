# Monitoring Service Design and Metrics Workflow
## Purpose
The Monitoring Service is the core observability component of EdgeCloud Monitor. It collects, stores, processes, and exposes monitoring data for backend services and edge devices.
Its main responsibilities are:
- registering backend services for monitoring
- checking service health and availability
- measuring response latency
- receiving edge telemetry metrics
- storing monitoring data in `monitoring_db`
- exposing historical metrics for dashboards
- supporting future Alert Service integration
## Service Registration Workflow
The Monitoring Service allows backend services to be registered as monitoring targets.
Endpoint:
```http
POST /api/v1/monitoring/services

Example request:

{
  "serviceName": "device-service",
  "serviceUrl": "http://device-service:8083"
}

Workflow:

1. A service registration request is submitted.
2. The request payload is validated.
3. Duplicate service names are checked.
4. The service is stored in the monitored_services table.
5. The service becomes available for health monitoring.

Health Monitoring Workflow

The health monitoring workflow checks registered services and records their operational state.

Endpoint:

POST /api/v1/monitoring/health-checks

Workflow:

1. Monitoring Service loads registered services from monitoring_db.
2. Each target service health endpoint is contacted.
3. Response time is measured.
4. The service is marked as UP or DOWN.
5. Monitoring results are stored in the service_metrics table.
6. The current service status is updated in monitored_services.

Stored service metric fields include:

* serviceId
* responseTimeMs
* statusCode
* uptimeStatus
* recordedAt

Telemetry Ingestion Workflow

The telemetry workflow receives metrics from Raspberry Pi devices or simulated edge agents.

Endpoint:

POST /api/v1/monitoring/telemetry

Example request:

{
  "deviceId": "pi-node-01",
  "cpuUsage": 45.5,
  "memoryUsage": 60.2,
  "temperature": 51.4
}

Workflow:

1. Edge device or simulated agent submits telemetry.
2. Request validation is applied.
3. CPU usage, memory usage, temperature, device ID, heartbeat status, and timestamp are stored.
4. Telemetry data becomes available for historical analysis and dashboard visualisation.

Stored telemetry fields include:

* deviceId
* cpuUsage
* memoryUsage
* temperature
* heartbeatStatus
* recordedAt

Historical Metrics Retrieval

Historical monitoring data is exposed for dashboard visualisation, troubleshooting, and future analytics.

Endpoint:

GET /api/v1/monitoring/history

The response includes:

* service health history
* response latency history
* telemetry history
* CPU usage
* memory usage
* temperature
* heartbeat status
* recorded timestamps

Results are ordered by recorded timestamp so that the newest monitoring records are returned first.

Database Ownership

The Monitoring Service owns the monitoring_db database.

Main tables:

Table	Purpose
monitored_services	Stores services registered for monitoring
service_metrics	Stores health check results and latency measurements
telemetry_metrics	Stores edge device telemetry records

No other service accesses monitoring_db directly. Other services must communicate with the Monitoring Service through APIs.

API Endpoints

Method	Endpoint	Purpose
POST	/api/v1/monitoring/services	Register a backend service for monitoring
POST	/api/v1/monitoring/health-checks	Execute health checks for registered services
POST	/api/v1/monitoring/telemetry	Receive edge telemetry metrics
GET	/api/v1/monitoring/history	Retrieve historical monitoring and telemetry data

Dashboard Integration

The React Dashboard will consume Monitoring Service APIs to display:

* service availability
* service status cards
* response latency
* CPU usage
* memory usage
* temperature
* historical charts
* edge device activity

Alert Service Integration

The Alert Service can later use Monitoring Service data to detect operational issues.

Potential alert conditions include:

* service down
* high response latency
* device offline
* high CPU usage
* high memory usage
* high temperature

Testing Evidence

Monitoring Service functionality was validated using curl, Postman-style API testing, Docker Compose, Eureka, and MySQL database checks.

Evidence collected includes:

* successful service registration response
* duplicate service registration response
* health check execution response
* telemetry ingestion response
* historical metrics response
* invalid request validation responses
* monitored_services database records
* service_metrics database records
* telemetry_metrics database records
* Docker container health output
* Eureka service registration screenshot
* API Gateway route validation output

Conclusion

The Monitoring Service provides the observability foundation of EdgeCloud Monitor. It supports service registration, service health monitoring, latency tracking, telemetry ingestion, historical metrics retrieval, dashboard integration, and future alert generation.

