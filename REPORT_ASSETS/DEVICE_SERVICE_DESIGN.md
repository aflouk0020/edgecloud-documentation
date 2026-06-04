

# Device Service Design and Heartbeat Workflow

## Purpose

The Device Service is responsible for managing registered edge devices in EdgeCloud Monitor.

It provides the backend foundation for device registration, heartbeat tracking, online and offline status management, and device metadata retrieval. This allows Raspberry Pi nodes and simulated edge devices to be tracked by the platform and later visualised in the React dashboard.

## Main Responsibilities

The Device Service is responsible for:

- registering edge devices
- storing device metadata
- tracking device heartbeat messages
- updating device online status
- detecting offline devices
- exposing registered devices through APIs
- supporting Monitoring Service telemetry correlation
- supporting future Alert Service offline device alerts
- supporting React dashboard device status views

## Device Registration Workflow

Endpoint:

```http
POST /api/v1/devices/register
```

Example request:

```json
{
  "deviceName": "raspberry-pi-01",
  "deviceType": "RaspberryPi",
  "ipAddress": "192.168.1.50"
}
```

Workflow:

1. A device registration request is submitted.
2. The request payload is validated.
3. The service checks whether the device name already exists.
4. A new device record is created.
5. The device is stored in `device_db`.
6. The device status is initially stored as `OFFLINE`.
7. A response containing the generated device ID and metadata is returned.

Stored fields include:

- id
- deviceName
- deviceType
- ipAddress
- status
- registeredAt
- lastHeartbeat

## Duplicate Device Handling

If a device is already registered with the same device name, the service returns a safe conflict response.

Expected status:

```http
HTTP/1.1 409 Conflict
```

This prevents duplicate device records and keeps the device registry consistent.

## Heartbeat Workflow

Endpoint:

```http
POST /api/v1/devices/heartbeat
```

Example request:

```json
{
  "deviceId": "device-uuid",
  "timestamp": "2026-06-04T16:10:00"
}
```

Workflow:

1. A registered device sends a heartbeat request.
2. The request validates the device ID.
3. The service searches for the matching device in `device_db`.
4. If the device exists, `lastHeartbeat` is updated.
5. The device status is set to `ONLINE`.
6. The updated device metadata is returned.

If the device does not exist, a safe error response is returned.

Expected unknown device status:

```http
HTTP/1.1 404 Not Found
```

## Offline Detection Workflow

Endpoint:

```http
POST /api/v1/devices/status/evaluate
```

Offline detection checks whether registered devices have missed heartbeats.

Configuration:

```yaml
edgecloud:
  device:
    offline-threshold-seconds: ${DEVICE_OFFLINE_THRESHOLD_SECONDS:60}
```

Workflow:

1. The service loads registered devices.
2. The current time is compared with each device `lastHeartbeat`.
3. If the heartbeat is older than the configured threshold, the device is marked `OFFLINE`.
4. Devices already offline remain offline.
5. Devices with recent heartbeat activity remain online.
6. Updated status is exposed through the device list API.

## Device Retrieval Workflow

Endpoint:

```http
GET /api/v1/devices
```

This endpoint returns all registered devices with their current metadata.

Returned fields include:

- id
- deviceName
- deviceType
- ipAddress
- status
- registeredAt
- lastHeartbeat

This response structure supports dashboard device cards, device status tables, and future alert views.

## Database Ownership

The Device Service owns the `device_db` database.

Main table:

| Table | Purpose |
|---|---|
| edge_devices | Stores registered device metadata, status, registration time, and heartbeat timestamp |

No other service directly accesses `device_db`. Other services must communicate with the Device Service through APIs.

## API Endpoints

| Method | Endpoint | Purpose |
|---|---|---|
| POST | /api/v1/devices/register | Register a new edge device |
| POST | /api/v1/devices/heartbeat | Process device heartbeat and update online status |
| GET | /api/v1/devices | Retrieve registered devices and current status |
| POST | /api/v1/devices/status/evaluate | Evaluate heartbeat age and update offline status |

## Monitoring Service Integration

The Monitoring Service stores telemetry metrics using logical device identifiers.

The Device Service provides the device registry and status information required to understand whether telemetry data belongs to a known edge device.

## Alert Service Integration

The Alert Service can later use device status values to generate alerts such as:

- device offline
- missed heartbeat
- stale telemetry
- edge node unavailable

## Edge Telemetry Agent Integration

The Python Edge Telemetry Agent will use the Device Service to:

1. register itself as an edge device
2. send heartbeat updates
3. allow the platform to track whether the agent is online
4. support telemetry association with device identity

## React Dashboard Integration

The React dashboard will use the Device Service to display:

- registered devices
- online and offline status
- device type
- IP address
- last heartbeat timestamp
- device availability cards
- device monitoring tables

## Testing Evidence

Device Service functionality was validated using curl/Postman-style API testing, Docker Compose, Eureka, and MySQL database checks.

Evidence collected includes:

- successful device registration response
- duplicate device response
- heartbeat success response
- invalid heartbeat response
- device list response
- offline detection response
- updated OFFLINE device status
- Docker container health output
- Eureka service registration output
- API Gateway route validation response
- `device_db` persistence records

## Conclusion

The Device Service provides the core edge device management capability of EdgeCloud Monitor. It supports device registration, heartbeat tracking, online and offline status management, device retrieval, dashboard integration, telemetry correlation, and future alert generation.