---
title: "Impersonate User"
weight: 3
menu:
  oem:
    parent: "portal_api_reference_admin"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/portal/v1/admin/impersonateUser" title="Impersonate User" request=`POST https://<your-host>:9909/api/portal/v1/admin/impersonateUser
Authorization: Bearer <token>
Content-Type: application/json

{
    "userId": "b2c3d4e5-f6a7-8901-bcde-f12345678901"
}` response=`Status Code: 200 OK
Response Body:
{
    "token": {
        "id": "f3a1c0d4e5b6a7c8d9e0f1a2b3c4d5e6",
        "userId": "b2c3d4e5-f6a7-8901-bcde-f12345678901"
    },
    "user": {
        "id": "b2c3d4e5-f6a7-8901-bcde-f12345678901",
        "email": "operator@example.com",
        "isAdmin": false,
        "isAccountOwner": false,
        "account": {
            "id": "c3d4e5f6-a7b8-9012-cdef-123456789012",
            "name": "Default"
        }
    }
}` %}}

Mint a new session token belonging to the user with the given `userId`. Use the returned token in subsequent requests to interact with the API as that user.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header. **The user must have admin privileges**, indicated by `isAdmin: true` on the user record.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token belonging to an admin user.

<b>Request Body</b>

The request body should be JSON-encoded.

- **userId**: The `id` of the user to impersonate.

<b>Response Schema</b>

On success, the endpoint returns a session token and user record for the impersonated user. The shape matches the response of [Login](/oem/portal-api-reference/authentication/login/).

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing, the token is not valid, or the user does not have admin privileges.
- **404 Not Found**: No user exists with the given `userId`.

{{% /apiEndpointCard %}}
