# Device Offline Detection Workflow

## Purpose

The Device Service supports offline detection for registered edge devices in EdgeCloud Monitor.

This feature checks device heartbeat activity and updates device availability status when a device has not communicated within the configured timeout threshold.

## Configuration

Offline detection uses a configurable threshold value.

yaml edgecloud:   device:     offline-threshold-seconds: ${DEVICE_OFFLINE_THRESHOLD_SECONDS:60} 

For development testing, the default threshold is 60 seconds.

## Workflow

1. A registered device sends heartbeat messages to the Device Service.
2. The Device Service stores the latest heartbeat timestamp.
3. The offline evaluation endpoint is triggered.
4. The service compares each device lastHeartbeat value against the configured threshold.
5. If the heartbeat is older than the threshold, the device is marked OFFLINE.
6. Updated device status is returned through the device retrieval API.

## Endpoint

http POST /status/evaluate 

This endpoint runs offline detection for registered devices.

Expected successful response:

http HTTP/1.1 204 No Content 

## Status Behaviour

| Condition | Result |
|---|---|
| Device has recent heartbeat | Remains ONLINE |
| Device heartbeat is older than threshold | Updated to OFFLINE |
| Device is already OFFLINE | Remains OFFLINE |

## Evidence Collected

Evidence collected for SCRUM-57 included:

- Device Service startup logs
- Eureka registration logs
- MySQL connection logs
- Offline evaluation API response
- Hibernate update statement
- Application log confirming offline detection
- Device retrieval response showing updated OFFLINE status

Example log:

text Device marked OFFLINE due to missed heartbeat 

## Dashboard and Alert Integration

This workflow supports future dashboard and alert functionality.

The React dashboard can use the device list API to show:

- online devices
- offline devices
- last heartbeat time
- device availability state

The Alert Service can later use this status to generate offline device alerts.

## Conclusion

Offline detection improves EdgeCloud Monitor by allowing the platform to identify inactive edge devices. This provides the foundation for device availability monitoring, dashboard status indicators, and future alert generation.