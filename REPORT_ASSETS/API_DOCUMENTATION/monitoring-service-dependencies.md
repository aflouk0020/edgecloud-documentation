# Monitoring Service Maven Dependencies

## Overview

The Monitoring Service uses Spring Boot and Spring Cloud dependencies to support monitoring, telemetry processing, service discovery, persistence, and operational visibility.

---

## Core Dependencies

### Spring Web

Provides REST API functionality.

Dependency:

spring-boot-starter-web

---

### Spring Data JPA

Provides database persistence support.

Dependency:

spring-boot-starter-data-jpa

---

### Validation

Provides DTO validation.

Dependency:

spring-boot-starter-validation

---

### Spring Boot Actuator

Provides health and monitoring endpoints.

Dependency:

spring-boot-starter-actuator

---

### Eureka Client

Registers the Monitoring Service with Eureka Service Discovery.

Dependency:

spring-cloud-starter-netflix-eureka-client

---

### MySQL Driver

Provides connectivity to monitoring_db.

Dependency:

mysql-connector-j

---

### Spring Boot Admin

Provides monitoring dashboard support.

Dependency:

spring-boot-admin-starter-server

---

## Java Version

Java 21

---

## Build Validation

The Monitoring Service successfully compiles using Maven.

Validation command:

mvn clean install