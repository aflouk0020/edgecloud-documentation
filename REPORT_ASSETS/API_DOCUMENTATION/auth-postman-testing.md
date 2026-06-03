# SCRUM-39 Authentication API Validation

## Registration Test
Status: Passed
HTTP Status: 201 Created

## Duplicate Registration Test
Status: Passed
HTTP Status: 409 Conflict

## Login Test
Status: Passed
HTTP Status: 200 OK

## Invalid Login Test
Status: Passed
HTTP Status: 401 Unauthorized

## Token Validation Test
Status: Passed
HTTP Status: 200 OK

## Invalid Token Test
Status: Passed
HTTP Status: 401 Unauthorized

## Gateway Routing Test
Status: Passed

All authentication endpoints were successfully accessed through the API Gateway.

Gateway URL:

http://localhost:8095/api/v1/auth/**
