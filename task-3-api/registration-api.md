## User Registration API
### HTTP Method

POST

### URL

/api/v1/auth/register

### Content Type

application/json

### Request Parameters

| Field | Type | Required | Constraints | Description |
|---|---|---|---|---|
| firstName | string | yes | 2-50 alphabetic characters | User first name |
| lastName | string | yes | 2-50 alphabetic characters | User last name |
| username | string | yes | unique, 3-30 chars, latin letters and digits only | Unique user login |
| password | string | yes | minimum 8 chars, must contain uppercase, lowercase, digit and special character | User password |
| captchaToken | string | yes | must be verified by CAPTCHA provider | CAPTCHA verification token |

## Validation Rules

- firstName and lastName must contain alphabetic characters only
- username must be unique
- password must meet security requirements
- captchaToken must be validated before user creation

## Success Response

### HTTP 201 Created

{
  "userId": "550e8400-e29b-41d4-a716-446655440000",
  "username": "ivan",
  "status": "created",
  "createdAt": "2026-05-26T12:00:00Z",
  "message": "User successfully registered"
}

## Error Responses

### 400 Bad Request

Possible reasons:
- Validation error
- Invalid captcha

{
  "errorCode": "VALIDATION_ERROR",
  "message": "Password does not meet security requirements"
}

{
  "errorCode": "INVALID_CAPTCHA",
  "message": "Captcha validation failed"
}

### 409 Conflict

{
  "errorCode": "USERNAME_ALREADY_EXISTS",
  "message": "Username already exists"
}

### 429 Too Many Requests

{
  "errorCode": "TOO_MANY_REQUESTS",
  "message": "Too many registration attempts. Please try again later."
}

### 500 Internal Server Error

{
  "errorCode": "INTERNAL_SERVER_ERROR",
  "message": "Unexpected backend error"
}


## Example Request

{
  "firstName": "Ivan",
  "lastName": "Ivanov",
  "username": "ivan",
  "password": "StrongPass123!",
  "captchaToken": "captcha-response-token"
}

## Example Success Response
 
{
  "userId": "550e8400-e29b-41d4-a716-446655440000",
  "username": "ivan",
  "status": "created",
  "createdAt": "2026-05-26T12:00:00Z",
  "message": "User successfully registered"
}

## Example Error Response

{
  "errorCode": "PASSWORD_VALIDATION_ERROR",
  "message": "Password must contain uppercase letter, digit and special character"
}

## Request Headers

| Header | Required | Value |
|---|---|---|
| Content-Type | yes | application/json |

## Response Headers

| Header | Value |
|---|---|
| Content-Type | application/json |