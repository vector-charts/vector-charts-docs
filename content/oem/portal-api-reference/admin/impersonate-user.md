---
title: "Impersonate User"
weight: 6
menu:
  oem:
    parent: "portal_api_reference_admin"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/portal/v1/admin/impersonateUser" title="Impersonate User" request=`POST https://<your-host>:9909/api/portal/v1/admin/impersonateUser
Authorization: Bearer <token>
Content-Type: application/json

{
    "userId": 7
}` response=`Status Code: 200 OK
Response Body:
{
    "user": {
        "id": 7,
        "accountId": 42,
        "email": "example@zydromarine.com",
        "isAdmin": false,
        "createdAt": 1736942400000,
        "modifiedAt": 1736942400000
    },
    "token": {
        "id": "f3a1c0d4e5b6a7c8d9e0f1a2b3c4d5e6",
        "userId": 7
    }
}` %}}

Issue a fresh session token for another user. The returned token authenticates subsequent Portal API requests as that user, allowing an administrator to act on their behalf for support and debugging.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token belonging to an administrator.

<b>Request Body</b>

The request body should be JSON-encoded.

- **userId**: The `id` of the user to impersonate.

<b>Response Schema</b>

On success, the endpoint returns the impersonated user and a new session token.

- `user`: The impersonated user record. See [Get User](/oem/portal-api-reference/admin/get-user/) for the field descriptions.
- `token`: The new session token. Its `id` field is the bearer string to send in the `Authorization` header to act as the impersonated user. The token behaves like one obtained from the [login endpoint](/oem/portal-api-reference/authentication/login/) and remains valid until it is invalidated through [logout](/oem/portal-api-reference/authentication/logout/).

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **403 Forbidden**: The authenticated user is not an administrator.
- **404 Not Found**: No user exists with the given `userId`.

{{% /apiEndpointCard %}}
