SCRUM-67 Simulated Telemetry Mode Validation

1. Overview

SCRUM-67 focused on validating the simulated telemetry mode capability of the Edge Telemetry Agent.

The objective was to ensure that EdgeCloud Monitor can continue development, testing, demonstrations, and integration activities even when Raspberry Pi hardware is unavailable or unstable.

Simulated mode allows the Edge Telemetry Agent to generate realistic telemetry metrics and heartbeat messages without requiring physical edge hardware.

Validation confirmed successful telemetry generation, telemetry submission, heartbeat transmission, backend processing, and database persistence.

⸻

2. Objective

The primary objectives of this validation activity were:

* Validate simulated telemetry generation.
* Validate simulated heartbeat generation.
* Verify Monitoring Service integration.
* Verify Device Service integration.
* Verify database persistence.
* Verify API communication.
* Verify operational logging.
* Reduce dependency on physical Raspberry Pi hardware.

⸻

3. Environment

Edge Agent

Component	Value
Language	Python 3
Runtime	Local Development Environment
Communication	REST APIs
Simulation Mode	Enabled
Telemetry Interval	5 Seconds

Backend Platform

Component	Port
API Gateway	8095
Monitoring Service	8082
Device Service	8083
Discovery Service	8761
monitoring_db	MySQL
device_db	MySQL

⸻

4. Simulated Mode Configuration

The Edge Telemetry Agent was executed using simulated mode.

Example configuration:

export EDGE_DEVICE_ID=dc4a1a0a-1d7d-45d9-b91d-c5bfae7653f7
export MONITORING_SERVICE_URL=http://localhost:8082/telemetry
export DEVICE_SERVICE_URL=http://localhost:8083/heartbeat
export SIMULATION_MODE=true
export TELEMETRY_INTERVAL_SECONDS=5

The agent was started using:

python main.py

⸻

5. Simulated Telemetry Validation

When simulation mode was enabled, telemetry metrics were generated automatically.

Example generated telemetry:

{
  "deviceId": "dc4a1a0a-1d7d-45d9-b91d-c5bfae7653f7",
  "cpuUsage": 30.48,
  "memoryUsage": 67.61,
  "temperature": 74.1
}

Additional generated values:

{
  "deviceId": "dc4a1a0a-1d7d-45d9-b91d-c5bfae7653f7",
  "cpuUsage": 84.14,
  "memoryUsage": 64.96,
  "temperature": 62.6
}

The generated values remained within realistic operational ranges.

Simulated Ranges

Metric	Expected Range
CPU Usage	5% – 95%
Memory Usage	20% – 90%
Temperature	35°C – 75°C

Validation confirmed successful simulated metric generation.

⸻

6. Telemetry Submission Validation

The generated telemetry was successfully submitted to the Monitoring Service.

Observed terminal output:

Telemetry POST status: 201
Telemetry submitted successfully

Validation confirmed:

* REST communication functioning correctly.
* Monitoring Service receiving telemetry.
* Successful HTTP responses.
* No runtime failures.

⸻

7. Heartbeat Validation

Heartbeat transmission continued to operate normally while simulation mode was enabled.

Observed terminal output:

Heartbeat POST status: 200
Heartbeat submitted successfully

Validation confirmed:

* Device Service communication.
* Heartbeat processing.
* Device status updates.
* Timestamp updates.

⸻

8. Monitoring Database Verification

Telemetry persistence was verified directly within monitoring_db.

Validation query:

SELECT device_id,
       cpu_usage,
       memory_usage,
       temperature,
       heartbeat_status,
       recorded_at
FROM telemetry_metrics
WHERE device_id='dc4a1a0a-1d7d-45d9-b91d-c5bfae7653f7'
ORDER BY recorded_at DESC
LIMIT 5;

Example stored results:

CPU	Memory	Temperature	Status
84.14	64.96	62.6	ONLINE
30.48	67.61	74.1	ONLINE

Validation confirmed successful persistence of simulated telemetry records.

⸻

9. Device Database Verification

Heartbeat persistence was verified within device_db.

Validation query:

SELECT id,
       device_name,
       status,
       last_heartbeat
FROM edge_devices;

Observed result:

heartbeat-pi-01
ONLINE
2026-06-16 10:23:56

Validation confirmed:

* ONLINE status updates.
* Heartbeat timestamp updates.
* Device tracking functionality.

⸻

10. End-to-End Workflow

The following workflow was successfully validated:

Edge Telemetry Agent
        │
        ▼
Simulated Telemetry Generation
        │
        ▼
Monitoring Service
        │
        ▼
monitoring_db

Heartbeat workflow:

Edge Telemetry Agent
        │
        ▼
Simulated Heartbeat Generation
        │
        ▼
Device Service
        │
        ▼
device_db

⸻

11. Acceptance Criteria Validation

Acceptance Criteria	Status
AC1 Simulated Mode Configurable	PASS
AC2 Simulated CPU Data Generated	PASS
AC3 Simulated Memory Data Generated	PASS
AC4 Simulated Temperature Data Generated	PASS
AC5 Simulated Heartbeat Supported	PASS
AC6 Backend Integration Works	PASS

⸻

12. Conclusion

SCRUM-67 was completed successfully.

The Edge Telemetry Agent can operate in simulated mode without requiring Raspberry Pi hardware. Simulated CPU, memory, temperature, and heartbeat data were generated successfully and processed by backend services. Validation confirmed successful telemetry persistence within monitoring_db, successful heartbeat processing within device_db, ONLINE status updates, and reliable backend integration.

This capability significantly reduces hardware dependency risk and enables continued development, testing, demonstrations, and validation activities throughout the EdgeCloud Monitor project lifecycle.