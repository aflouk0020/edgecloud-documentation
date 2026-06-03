# Sprint 1 Docker Deployment and Infrastructure Workflow

## Overview

This document describes the Sprint 1 deployment architecture for the EdgeCloud Monitor platform.

Sprint 1 introduced the first containerised cloud-native deployment environment using Docker Compose, Eureka Service Discovery, Spring Cloud Gateway, Authentication Service, and MySQL.

The objective was to create a reproducible distributed infrastructure that supports service communication, service discovery, authentication, and future platform expansion.

---

## Sprint 1 Infrastructure Components

The Sprint 1 deployment environment consists of the following containers:

### Discovery Service

Container:

edgecloud-discovery-service

Responsibilities:

- Service registration
- Service discovery
- Availability tracking
- Dynamic lookup of backend services

---

### API Gateway

Container:

edgecloud-api-gateway

Responsibilities:

- Centralised API entry point
- Request routing
- Service forwarding
- Future JWT validation
- Error handling

---

### Authentication Service

Container:

edgecloud-auth-service

Responsibilities:

- User registration
- User login
- JWT generation
- JWT validation
- Role management

---

### Authentication Database

Container:

auth-mysql

Responsibilities:

- User persistence
- Credential storage
- Role storage
- Authentication data management

---

## Docker Compose Architecture

The deployment environment is orchestrated using Docker Compose.

Container communication occurs through a shared Docker network.

Architecture:

Client

↓

API Gateway

↓

Authentication Service

↓

MySQL Database

All backend services register with Eureka during startup.

---

## Docker Network Architecture

Network Name:

edgecloud-network

All containers are attached to the same Docker network.

This allows containers to communicate using service names instead of IP addresses.

Examples:

- edgecloud-discovery-service
- edgecloud-api-gateway
- edgecloud-auth-service
- auth-mysql

Benefits:

- Simplified communication
- Dynamic service discovery
- Reduced configuration complexity
- Portable deployment

---

## Service Startup Workflow

Recommended startup sequence:

### Step 1

Start Discovery Service

Purpose:

Provides service registration infrastructure.

---

### Step 2

Start Database Containers

Purpose:

Provides persistent storage for backend services.

---

### Step 3

Start API Gateway

Purpose:

Provides routing infrastructure.

---

### Step 4

Start Authentication Service

Purpose:

Registers with Eureka and connects to auth_db.

---

## Docker Compose Startup Command

Deployment command:

```bash
docker compose up
```

Verification commands:

```bash
docker ps
```

```bash
docker logs <container-name>
```

```bash
docker network ls
```

---

## Eureka Service Registration Workflow

Each backend service automatically registers with Eureka during startup.

Registration sequence:

Service Startup

↓

Eureka Registration

↓

Health Check Validation

↓

Service Available for Discovery

Examples:

- EDGECLOUD-AUTH-SERVICE
- EDGECLOUD-API-GATEWAY

Benefits:

- Dynamic service discovery
- Improved scalability
- Reduced dependency on fixed addresses

---

## API Gateway Communication Workflow

All client requests enter the platform through the API Gateway.

Example request flow:

Client Request

↓

API Gateway

↓

Eureka Lookup

↓

Authentication Service

↓

Response Returned

Gateway route:

```http
/api/v1/auth/**
```

The gateway forwards requests using Eureka logical service names.

Example:

```text
lb://EDGECLOUD-AUTH-SERVICE
```

---

## Authentication Service Deployment

The Authentication Service is deployed as a Docker container.

Deployment responsibilities:

- Connect to auth-mysql
- Register with Eureka
- Accept routed gateway requests
- Generate JWT tokens
- Validate JWT tokens

Database connectivity is established using Docker service-name communication.

Example database host:

```text
auth-mysql
```

---

## Infrastructure Validation

The following validation activities were completed during Sprint 1.

### Docker Validation

Verified:

- Container startup success
- Container health
- Docker networking
- Service availability

---

### Eureka Validation

Verified:

- Service registration
- Service discovery
- Multi-service visibility

---

### API Gateway Validation

Verified:

- Route forwarding
- Service lookup
- Error handling

---

### Authentication Validation

Verified:

- Registration
- Login
- JWT generation
- JWT validation

---

## Deployment Evidence

Associated evidence is stored within:

REPORT_ASSETS/DEPLOYMENT_IMAGES

and the Sprint 1 OneDrive evidence repository.

Evidence includes:

- Docker Compose startup screenshots
- Docker container screenshots
- Eureka dashboard screenshots
- API Gateway validation screenshots
- Authentication workflow screenshots
- Database connectivity screenshots

---

## Conclusion

Sprint 1 successfully established the first cloud-native deployment environment for EdgeCloud Monitor.

Docker Compose, Eureka Service Discovery, API Gateway routing, Authentication Service deployment, and MySQL persistence were integrated and validated. The deployment architecture provides a stable foundation for future Monitoring Service, Device Service, Alert Service, dashboard integration, and full platform deployment.