SCRUM-66 Raspberry Pi Compatibility Validation

Overview

SCRUM-66 focused on validating Raspberry Pi compatibility for the Edge Telemetry Agent within the EdgeCloud Monitor platform.

The objective was to verify that the Python-based Edge Telemetry Agent could execute successfully on physical Raspberry Pi hardware, collect telemetry metrics, communicate with backend microservices, submit heartbeat information, and persist monitoring data within platform databases.

Testing was performed using a physical Raspberry Pi running Raspberry Pi OS Bookworm and connected to the local EdgeCloud Monitor environment hosted on a development workstation.

⸻

Validation Environment

Raspberry Pi Environment

Component	Value
Device	Raspberry Pi
Operating System	Raspberry Pi OS Bookworm
Kernel	Linux 6.12.62+rpt-rpi-v8
Architecture	aarch64
Python Version	Python 3.11.2
Git Version	2.39.5

EdgeCloud Monitor Environment

Component	Port
API Gateway	8095
Monitoring Service	8082
Device Service	8083
Eureka Discovery	8761
Monitoring Database	3308
Device Database	3309

⸻

Validation Activities

Agent Startup Validation

The Edge Telemetry Agent was executed successfully on the Raspberry Pi without runtime failures.

Observed output:

Starting Edge Telemetry Agent
Telemetry interval: 5 seconds

Result:

PASS

⸻

Telemetry Collection Validation

The agent successfully collected operational metrics from the Raspberry Pi.

Observed telemetry payload:

{
  "deviceId": "dc4a1a0a-1d7d-45d9-b91d-c5bfae7653f7",
  "cpuUsage": 0.2,
  "memoryUsage": 6.1,
  "temperature": 31.64
}

Metrics successfully collected:

* CPU utilisation
* Memory utilisation
* Temperature

Result:

PASS

⸻

Telemetry Submission Validation

Telemetry data was successfully transmitted to the Monitoring Service.

Observed response:

Telemetry POST status: 201
Telemetry submitted successfully

Flow validated:

Raspberry Pi
        ↓
Edge Telemetry Agent
        ↓
Monitoring Service
        ↓
monitoring_db

Result:

PASS

⸻

Heartbeat Submission Validation

Heartbeat messages were successfully transmitted to the Device Service.

Observed response:

Heartbeat POST status: 200
Heartbeat submitted successfully

Flow validated:

Raspberry Pi
        ↓
Edge Telemetry Agent
        ↓
Device Service
        ↓
device_db

Result:

PASS

⸻

Database Verification

Monitoring Database Evidence

Query executed:

SELECT device_id,
       cpu_usage,
       memory_usage,
       temperature,
       heartbeat_status,
       recorded_at
FROM telemetry_metrics
WHERE device_id = 'dc4a1a0a-1d7d-45d9-b91d-c5bfae7653f7'
ORDER BY recorded_at DESC
LIMIT 5;

Result:

Telemetry records were successfully persisted.

Example values:

CPU	Memory	Temperature	Status
0.5	6.1	32.62	ONLINE
0.3	6.1	32.62	ONLINE
0.2	6.1	31.64	ONLINE

Result:

PASS

⸻

Device Database Evidence

Query executed:

SELECT id,
       device_name,
       status,
       last_heartbeat
FROM edge_devices;

Result:

device_name: heartbeat-pi-01
status: ONLINE
last_heartbeat: 2026-06-16 10:12:57

The heartbeat timestamp was updated successfully and the device remained ONLINE.

Result:

PASS

⸻

Failure Handling Validation

Initial testing intentionally used invalid endpoint configurations.

Observed behaviour:

* Telemetry submission failures were logged.
* Heartbeat submission failures were logged.
* Agent execution continued.
* No application crashes occurred.

Example error:

Failed to establish a new connection
Connection refused

Result:

PASS

⸻

Acceptance Criteria Validation

Acceptance Criteria	Status
AC1 Python Agent Runs on Raspberry Pi	PASS
AC2 Telemetry Metrics Collected on Raspberry Pi	PASS
AC3 Telemetry Submission Verified	PASS
AC4 Heartbeat Submission Verified	PASS
AC5 Failure Behaviour Observed	PASS
AC6 Raspberry Pi Evidence Collected	PASS

⸻

Conclusion

SCRUM-66 successfully validated Raspberry Pi compatibility for the Edge Telemetry Agent. The agent executed correctly on physical Raspberry Pi hardware, collected operational telemetry metrics, submitted telemetry to the Monitoring Service, transmitted heartbeat messages to the Device Service, and persisted monitoring information within backend databases.

The validation confirms that EdgeCloud Monitor can support real edge-device monitoring workflows and establishes a verified foundation for future observability, alerting, dashboard visualisation, and edge-computing capabilities.