SCRUM-36 Security Configuration

Overview

Spring Security was configured for the Authentication Service to provide secure access control for public and protected endpoints.

Public Endpoints

The following endpoints are accessible without authentication:
POST /login
POST /register
GET /actuator/health
GET /actuator/info

Protected Endpoints

The following endpoints require authentication:
GET /validate

Future authenticated endpoints will also require valid JWT authentication.

Password Security

Passwords are stored using:
BCryptPasswordEncoder

Passwords are never stored in plain text.

Session Management

The Authentication Service uses:
SessionCreationPolicy.STATELESS

No server-side session state is maintained.

Security Testing Evidence

Verified:

* Login endpoint accessible without authentication
* Registration endpoint accessible without authentication
* Health endpoint accessible without authentication
* Protected endpoint returns HTTP 401 when unauthenticated

Example result:
GET /protected-test

HTTP/1.1 401 Unauthorized

Outcome

Security configuration successfully separates public and protected routes and provides a foundation for JWT-based authentication across EdgeCloud Monitor.
