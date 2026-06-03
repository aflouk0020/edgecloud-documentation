# Authentication Service

## Overview

The Authentication Service is responsible for managing user authentication and authorisation within the EdgeCloud Monitor platform.

The service provides secure user registration, user login, password hashing, JWT token generation, JWT validation, and role management.

The Authentication Service acts as the central security component for the platform and supports secure communication between users, the API Gateway, and backend microservices.

---

# Responsibilities

The Authentication Service is responsible for:

- User registration
- User login
- Password hashing
- JWT token generation
- JWT token validation
- User role management
- Authentication error handling
- Supporting API Gateway authentication workflows

---

# Authentication API Endpoints

## Register User

### Endpoint

```http
POST /api/v1/auth/register
```

### Example Request

```json
{
  "email": "admin@edgecloud.com",
  "password": "Password123",
  "role": "ADMIN"
}
```

### Example Response

```json
{
  "email": "admin@edgecloud.com",
  "message": "User registered successfully"
}
```

### Success Status Code

```http
201 Created
```

---

## Login User

### Endpoint

```http
POST /api/v1/auth/login
```

### Example Request

```json
{
  "email": "admin@edgecloud.com",
  "password": "Password123"
}
```

### Example Response

```json
{
  "token": "eyJhbGciOiJIUzI1NiJ9...",
  "role": "ADMIN"
}
```

### Success Status Code

```http
200 OK
```

---

## Validate Token

### Endpoint

```http
GET /api/v1/auth/validate
```

### Request Header

```http
Authorization: Bearer <token>
```

### Example Response

```json
{
  "valid": true,
  "email": "admin@edgecloud.com",
  "role": "ADMIN"
}
```

### Success Status Code

```http
200 OK
```

---

# JWT Authentication Workflow

The authentication workflow operates as follows:

1. A user registers an account.
2. The password is hashed using BCrypt before storage.
3. User details are stored in the Authentication Database.
4. The user submits login credentials.
5. The Authentication Service validates credentials.
6. A JWT token is generated.
7. The JWT token contains:
   - User email
   - User role
   - Issued timestamp
   - Expiry timestamp
8. The JWT token is returned to the frontend.
9. The frontend includes the token in protected requests.
10. Protected endpoints validate the JWT token before granting access.

---

# User Role Model

The platform currently supports three user roles.

## ADMIN

Administrative access to platform configuration and user management.

## OPERATOR

Operational access to monitoring features and platform management functions.

## VIEWER

Read-only access to monitoring dashboards and system information.

Roles are stored in the Authentication Database and included in JWT token claims.

---

# Password Security

Passwords are never stored in plain text.

The Authentication Service uses:

```text
BCryptPasswordEncoder
```

Security measures include:

- Password hashing before persistence
- Password verification through BCrypt matching
- No storage of raw passwords
- Secure authentication processing

---

# Authentication Error Handling

The Authentication Service provides consistent error responses.

Supported authentication error scenarios include:

- Invalid input
- Missing email
- Missing password
- Invalid email format
- Duplicate email registration
- Invalid credentials
- Unsupported role
- Expired JWT token
- Malformed JWT token
- Missing JWT token

Example response:

```json
{
  "timestamp": "2026-06-03T12:00:00",
  "status": 401,
  "error": "Unauthorized",
  "message": "Invalid credentials",
  "path": "/api/v1/auth/login"
}
```

---

# API Gateway Integration

The Authentication Service supports secure API Gateway integration.

Authentication requests are routed through:

```http
/api/v1/auth/**
```

The API Gateway can:

- Forward authentication requests
- Validate JWT tokens
- Protect backend services
- Support future role-based access control decisions

---

# Testing Evidence

Authentication functionality has been validated using Postman.

Validated scenarios include:

- Successful registration
- Duplicate email registration
- Successful login
- Invalid login
- JWT generation
- JWT validation
- Invalid JWT validation
- Security error responses

Testing screenshots and API response evidence are stored within the project testing evidence repository.

---

# Summary

The Authentication Service provides secure authentication, authorisation, JWT-based security, password protection, role management, and API Gateway integration for the EdgeCloud Monitor platform.