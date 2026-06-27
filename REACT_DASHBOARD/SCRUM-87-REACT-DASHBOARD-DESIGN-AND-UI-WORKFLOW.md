# SCRUM-87 — React Dashboard Design and UI Workflow

## Overview

The React Dashboard is the primary user interface for EdgeCloud Monitor.

It provides a modern web-based monitoring console that allows administrators to authenticate, view platform health, monitor services, inspect registered edge devices, analyse telemetry metrics, and respond to operational alerts through a single interface.

The dashboard communicates with backend microservices exclusively through the API Gateway, providing a clean separation between the frontend and backend architecture while supporting secure JWT-based authentication.

---

# Dashboard Responsibilities

The React Dashboard is responsible for:

- authenticating users
- storing and using JWT access tokens
- communicating with backend APIs through the API Gateway
- displaying platform overview information
- presenting service monitoring information
- displaying registered edge devices
- visualising telemetry metrics
- presenting operational alerts
- supporting alert resolution workflows
- providing responsive loading, empty and error states

---

# Technology Stack

The dashboard is implemented using:

- React
- Vite
- JavaScript
- React Router
- Axios
- CSS3
- JWT Authentication
- API Gateway integration
- Docker compatible deployment

---

# Frontend Folder Structure

The dashboard follows a modular frontend architecture.

Typical organisation includes:

```text
src/
    components/
    pages/
    services/
    hooks/
    context/
    router/
    assets/
    styles/
```

This structure separates presentation, API communication, routing and reusable components to improve maintainability.

---

# Authentication Workflow

User authentication follows a JWT-based workflow.

Authentication process:

1. User opens the Login page.
2. Credentials are submitted.
3. Login request is sent through the API Gateway.
4. Authentication Service validates credentials.
5. JWT token is returned.
6. Token is stored securely by the frontend.
7. Protected dashboard routes become available.
8. Logout removes the stored token and redirects the user to the login page.

---

# Protected Route Workflow

Protected pages require a valid authenticated session.

Protected pages include:

- Dashboard
- Services
- Devices
- Telemetry
- Alerts

Unauthenticated users are redirected to the Login page.

---

# API Gateway Integration

The React Dashboard never communicates directly with backend services.

All requests follow the architecture:

```text
React Dashboard
        ↓
API Gateway
        ↓
Backend Microservices
```

This provides:

- centralised routing
- simplified frontend configuration
- secure request handling
- scalable service discovery

---

# Backend API Endpoints

The dashboard currently integrates with:

POST /api/v1/auth/login

GET /api/v1/monitoring/services

GET /api/v1/monitoring/history

GET /api/v1/devices

GET /api/v1/alerts

PUT /api/v1/alerts/{id}/resolve

---

# Dashboard Navigation Workflow

The user interface provides the following navigation structure:

Login

↓

Dashboard

↓

System Overview

↓

Services

↓

Devices

↓

Telemetry

↓

Alerts

Each page is accessible through the sidebar navigation after successful authentication.

---

# Dashboard Views

## Login

Purpose

Authenticate administrators and obtain a JWT token.

Primary API

POST /api/v1/auth/login

---

## System Overview

Purpose

Provide a high-level operational summary of the platform.

Displayed information includes:

- registered devices
- online devices
- offline devices
- telemetry records
- monitored services
- active alerts

---

## Service Health

Purpose

Display operational health information for monitored backend services.

Data Source

GET /api/v1/monitoring/services

---

## Device Monitoring

Purpose

Display registered edge devices, heartbeat status and availability.

Data Source

GET /api/v1/devices

---

## Telemetry Metrics

Purpose

Display CPU usage, memory usage, temperature values and historical telemetry information.

Data Source

GET /api/v1/monitoring/history

---

## Active Alerts

Purpose

Display unresolved operational alerts and support incident resolution.

Data Source

GET /api/v1/alerts

Resolution API

PUT /api/v1/alerts/{id}/resolve

---

# Dashboard State Management

The frontend supports:

- loading indicators
- empty state messages
- API error handling
- refresh actions
- authenticated session management

These behaviours improve usability and operational reliability.

---

# Error Handling

The dashboard gracefully handles:

- authentication failures
- unavailable backend services
- API validation errors
- missing monitoring data
- empty telemetry history
- unavailable devices

Clear feedback is presented to users whenever requests cannot be completed successfully.

---

# Screenshot Evidence

Sprint 3 evidence includes:

- Login page
- Dashboard overview
- Service Health page
- Device Monitoring page
- Telemetry Metrics page
- Active Alerts page
- Alert resolution workflow
- API Gateway validation
- Postman testing evidence

---

# Validation Summary

The dashboard successfully demonstrates:

- JWT authentication
- API Gateway communication
- monitoring data retrieval
- device monitoring
- telemetry visualisation
- alert management
- responsive dashboard navigation
- frontend integration with backend services

---

# Conclusion

The React Dashboard provides a modern operational interface for EdgeCloud Monitor.

It integrates securely with backend microservices through the API Gateway, presents monitoring information through dedicated views, supports authenticated administration workflows, and forms the primary interface used throughout Sprint 3.

The implementation supports supervisor demonstrations, interim reporting, final dissertation documentation, and future platform expansion.
