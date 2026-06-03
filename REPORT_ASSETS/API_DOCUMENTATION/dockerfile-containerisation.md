# Dockerfile Containerisation Approach

## Purpose

This document describes the Dockerfile approach used to containerise the core backend services in EdgeCloud Monitor.

This supports SCRUM-41 by documenting how the Discovery Service, API Gateway, and Authentication Service are packaged and validated using Docker.

## Scope

Validated services:

- edgecloud-discovery-service
- edgecloud-api-gateway
- edgecloud-auth-service

The wider Docker Compose test also confirmed compatibility with:

- edgecloud-monitoring-service
- edgecloud-device-service
- edgecloud-alert-service

## Dockerfile Strategy

Each Spring Boot service follows the same containerisation workflow:

1. Build the service using Maven.
2. Package the service as an executable JAR.
3. Copy the JAR into a Java 21 runtime image.
4. Expose the correct service port.
5. Start the service using `java -jar app.jar`.

## Java 21 Runtime Image

The services use Java 21 compatible Eclipse Temurin images, for example:

```dockerfile
FROM eclipse-temurin:21-jre-alpine

or multi-stage builds using:

FROM eclipse-temurin:21-jdk
FROM eclipse-temurin:21-jre
This ensures consistency with the project’s Java 21 Spring Boot architecture.

Docker Compose Validation

The full backend stack was tested using:

docker compose --env-file ../env/.env up --build -d
The stack included:

* Discovery Service
* API Gateway
* Authentication Service
* Monitoring Service
* Device Service
* Alert Service
* Auth MySQL
* Monitoring MySQL
* Device MySQL
* Alert MySQL

The stack was stopped after testing using:
docker compose --env-file ../env/.env down
Startup Dependency Fix

The Authentication Service depends on Discovery Service and Auth MySQL.

To avoid startup timing errors, Docker Compose health-based dependencies were used:depends_on:
  discovery-service:
    condition: service_healthy
  auth-mysql:
    condition: service_healthy
    This ensures the Authentication Service starts only after Eureka and MySQL are healthy.

Validation Results

Docker Compose confirmed that the following images built successfully:

* compose-discovery-service
* compose-api-gateway
* compose-auth-service
* compose-monitoring-service
* compose-device-service
* compose-alert-service

Docker container health checks confirmed all backend containers started successfully.

Eureka Registration Evidence

The Eureka dashboard confirmed the following services registered successfully:

* EDGECLOUD-API-GATEWAY
* EDGECLOUD-AUTH-SERVICE
* EDGECLOUD-MONITORING-SERVICE
* EDGECLOUD-DEVICE-SERVICE
* EDGECLOUD-ALERT-SERVICE

Best Practices Applied

* Java 21 runtime images
* Service-specific Dockerfiles
* Docker Compose orchestration
* Environment-based configuration
* Health checks for readiness
* Docker network isolation
* No shared databases between services
* Container lifecycle validation

Conclusion

The core backend services have been successfully containerised and validated through Docker Compose.

The Discovery Service, API Gateway, and Authentication Service Dockerfiles exist and build successfully. The full backend stack also starts successfully through Docker Compose, with all services becoming healthy and registering with Eureka.

