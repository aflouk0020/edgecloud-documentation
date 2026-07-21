Edge Telemetry Agent Documentation

1. Introduction

Purpose

The Edge Telemetry Agent is a lightweight Python application responsible for collecting operational metrics from edge devices and transmitting them to the EdgeCloud Monitor platform.

The agent enables the platform to monitor remote devices such as Raspberry Pi systems and simulated edge environments by continuously sending telemetry and heartbeat information to backend microservices.

Responsibilities

The Edge Telemetry Agent is responsible for:

* Collecting CPU utilisation
* Collecting memory utilisation
* Collecting device temperature
* Generating heartbeat messages
* Sending telemetry data to the Monitoring Service
* Sending heartbeat data to the Device Service
* Logging operational events
* Handling temporary communication failures
* Supporting Raspberry Pi and simulated execution environments

⸻

2. Technology Stack

Component	Technology
Language	Python 3
HTTP Client	requests
Configuration	Environment Variables
Logging	logging module
Runtime	Raspberry Pi / Local Machine
Communication	REST APIs
Authentication	JWT
Deployment Target	Edge Device

⸻

3. Project Structure

Example:

edgecloud-edge-agent
│
├── main.py
├── requirements.txt
├── .env.example
│
└── src
    ├── config.py
    ├── telemetry_collector.py
    ├── telemetry_client.py
    ├── heartbeat_client.py

main.py

Responsible for:

* Startup
* Telemetry loop
* Heartbeat loop
* Logging
* Graceful shutdown

config.py

Responsible for:

* Loading configuration
* Environment variables

telemetry_collector.py

Responsible for:

* CPU metrics
* Memory metrics
* Temperature metrics

telemetry_client.py

Responsible for:

* Monitoring Service communication

heartbeat_client.py

Responsible for:

* Device Service communication

⸻

4. Configuration

The Edge Telemetry Agent is configured using environment variables.

Example Variables

DEVICE_ID=dc4a1a0a-1d7d-45d9-b91d-c5bfae7653f7
API_BASE_URL=http://localhost:8095
TELEMETRY_INTERVAL_SECONDS=5
SIMULATION_MODE=true

Description

Variable	Purpose
DEVICE_ID	Unique device identifier
API_BASE_URL	API Gateway URL
TELEMETRY_INTERVAL_SECONDS	Collection frequency
SIMULATION_MODE	Enables simulated metrics

⸻

5. Installation

Create Virtual Environment

python3 -m venv .venv

Activate Environment

source .venv/bin/activate

Install Dependencies

pip install -r requirements.txt

Dependencies

Package	Purpose
requests	REST API communication
python-dotenv	Environment variable loading
psutil	CPU and memory metric collection

⸻

6. Running the Agent

Example

export TELEMETRY_INTERVAL_SECONDS=5
python main.py

Expected Output

Starting Edge Telemetry Agent
Telemetry interval: 5 seconds
Collected telemetry payload
Telemetry submitted successfully
Heartbeat submitted successfully

⸻

7. Telemetry Workflow

Telemetry Collection

The agent periodically collects:

* CPU utilisation
* Memory utilisation
* Temperature

Telemetry Endpoint

POST /api/v1/monitoring/telemetry

Example Payload

{
  "deviceId": "dc4a1a0a-1d7d-45d9-b91d-c5bfae7653f7",
  "cpuUsage": 50.5,
  "memoryUsage": 60.2,
  "temperature": 45.1
}

Telemetry Submission

Collected telemetry is submitted through the API Gateway.

Data Flow

Edge Telemetry Agent
        │
        ▼
API Gateway
        │
        ▼
Monitoring Service
        │
        ▼
monitoring_db

⸻

8. Heartbeat Workflow

The heartbeat mechanism confirms that a device is online.

Heartbeat Endpoint

POST /api/v1/devices/heartbeat

Example Payload

{
  "deviceId": "dc4a1a0a-1d7d-45d9-b91d-c5bfae7653f7",
  "timestamp": "2026-06-13T16:45:00"
}

Data Flow

Edge Telemetry Agent
        │
        ▼
API Gateway
        │
        ▼
Device Service
        │
        ▼
device_db

⸻

9. Failure Handling

The Edge Telemetry Agent has been designed to continue operating when backend services become unavailable.

Monitoring Service Unavailable

Behaviour:

* Error logged
* Agent continues running
* Next interval retries automatically

Device Service Unavailable

Behaviour:

* Heartbeat failure logged
* Process remains operational
* Next cycle retries automatically

API Gateway Unavailable

Behaviour:

* Request failure logged
* Agent continues collecting metrics
* Future cycles attempt retransmission

Graceful Shutdown

Supported through:

KeyboardInterrupt

Expected behaviour:

Stopping Edge Telemetry Agent
Shutdown complete

⸻

10. Raspberry Pi vs Simulated Mode

Raspberry Pi Mode

Production-style deployment.

Metrics originate from:

* Actual CPU usage
* Actual memory usage
* Actual device temperature

Simulated Mode

Development and testing environment.

Metrics are generated programmatically to support:

* Development
* Integration testing
* Demonstrations
* Validation activities

⸻

11. Validation Evidence

SCRUM-64 End-to-End Validation Results

Successful validation confirmed the complete edge monitoring workflow.

Authentication Validation

Verified through:

POST /api/v1/auth/register
POST /api/v1/auth/login

Telemetry Validation Path

Edge Telemetry Agent
→ API Gateway
→ Monitoring Service
→ monitoring_db

Result:

201 Created

Heartbeat Validation Path

Edge Telemetry Agent
→ API Gateway
→ Device Service
→ device_db

Result:

200 OK

Database Validation

Monitoring Database:

SELECT * FROM telemetry_metrics;

Device Database:

SELECT id, device_name, status, last_heartbeat
FROM edge_devices;

Validation confirmed:

* Telemetry persistence
* Device registration
* ONLINE device status
* Heartbeat timestamp updates
* Successful API Gateway routing
* Successful service-to-service communication

Evidence Reference

Detailed validation evidence is available in:

REPORT_ASSETS/SCRUM-64-END-TO-END-VALIDATION.md

This evidence includes:

* Authentication validation
* API responses
* Telemetry submission verification
* Heartbeat submission verification
* Database verification
* End-to-end workflow testing
* Docker service validation

⸻

12. Future Enhancements

Potential future improvements include:

* MQTT-based telemetry transmission
* TLS-secured edge communications
* Device auto-registration
* Telemetry batching
* Offline buffering
* Edge anomaly detection
* Kubernetes deployment support
* Prometheus integration
* Grafana integration
* Real-time WebSocket dashboard updates

⸻

13. Conclusion

The Edge Telemetry Agent successfully demonstrates edge-to-cloud monitoring within the EdgeCloud Monitor platform.

Validation confirms that telemetry and heartbeat information can be collected from edge environments, transmitted through the API Gateway, processed by backend microservices, and persisted within platform databases.

The successful completion of SCRUM-64 establishes the foundation required for dashboard visualisation, device monitoring, alert generation, service observability, and future cloud-native monitoring enhancements.