# Authentication Service Role-Based Access Control

## Overview

The EdgeCloud Monitor Authentication Service implements Role-Based Access Control (RBAC) to support different permission levels across the platform.

RBAC ensures that authenticated users receive an assigned role which can later be used by the API Gateway and backend services to enforce access control policies.

The Authentication Service currently supports three platform roles:

- ADMIN
- OPERATOR
- VIEWER

These roles are stored during user registration and included within JWT tokens during authentication.

---

## Role Definitions

### ADMIN

Administrative users with full platform access.

Responsibilities:

- Manage platform users
- Configure system settings
- Access all monitoring resources
- Perform administrative operations

### OPERATOR

Operational users responsible for monitoring and management activities.

Responsibilities:

- Monitor platform services
- Manage operational workflows
- Review alerts and telemetry
- Access operational dashboards

### VIEWER

Read-only users with limited access.

Responsibilities:

- View monitoring dashboards
- Review telemetry information
- Access reporting features
- No administrative privileges

---

## User Registration with Roles

During account registration, users must provide a valid platform role.

### Registration Request

```json
{
  "email": "operator@example.com",
  "password": "Password123",
  "role": "OPERATOR"
}

Successful Registration Response

{
  "id": "1f9260c9-d975-45ee-9c10-58acfb4b6094",
  "email": "operator@example.com",
  "role": "OPERATOR"
}

Role Persistence

Roles are stored in the Authentication Service database.

Users Table Example

Email

Role

admin@example.com

ADMIN

operator@example.com

OPERATOR

viewer@example.com

VIEWER

The role information remains associated with the user account throughout the authentication lifecycle.

JWT Role Claims

When a user successfully logs in, the Authentication Service generates a JWT token containing user identity and role information.

JWT Claims

Claim

Description

sub

User email

role

Platform role

iat

Issued timestamp

exp

Expiration timestamp

Example Payload
{
  "sub": "operator@example.com",
  "role": "OPERATOR",
  "iat": 1748900000,
  "exp": 1748903600
}
⸻

Login Response

The authenticated role is returned as part of the login response.

Example Response

{
  "token": "jwt_token_here",
  "role": "OPERATOR"
}

This allows client applications and future services to understand the authenticated user’s permission level.
Invalid Role Handling

The Authentication Service validates role values during registration.

Supported roles:

* ADMIN
* OPERATOR
* VIEWER

Any unsupported role is rejected.

Invalid Registration Request

{
  "email": "user@example.com",
  "password": "Password123",
  "role": "MANAGER"
}

Error Response
{
  "timestamp": "2026-06-03T00:03:26",
  "status": 400,
  "error": "Bad Request",
  "message": "Invalid request body or unsupported role value",
  "path": "/register"
}


Future Role-Based Authorisation

The current implementation prepares the platform for future authorisation requirements.

Future enhancements may include:

* Gateway-level role enforcement
* Service-to-service role validation
* Endpoint-specific access restrictions
* Administrative management functions
* Fine-grained permission controls
Validation Results

The following functionality has been verified:

Feature

Status

ADMIN role defined

Complete

OPERATOR role defined

Complete

VIEWER role defined

Complete

Role stored during registration

Complete

Role persisted in auth_db

Complete

Role included in JWT token

Complete

Role returned in login response

Complete

Invalid role rejection

Complete

Postman/API validation testing

Complete

Conclusion

Role-Based Access Control has been successfully implemented within the EdgeCloud Monitor Authentication Service. User roles are validated, persisted, included within JWT tokens, and returned during authentication. This implementation provides the foundation for future platform-wide authorisation and secure access control.
