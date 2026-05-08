---
title: "Login"
weight: 1
menu:
  oem:
    parent: "portal_api_reference_authentication"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/portal/v1/auth/login" title="Login" request=`POST https://<your-host>:9909/api/portal/v1/auth/login
Content-Type: application/json

{
    "username": "admin",
    "password": "admin"
}` response=`Status Code: 200 OK
Response Body:
{
    "token": {
        "id": "f3a1c0d4e5b6a7c8d9e0f1a2b3c4d5e6",
        "userId": 1
    },
    "user": {
        "id": 1,
        "email": "admin",
        "isAdmin": true,
        "isAccountOwner": false,
        "account": {
            "id": 1,
            "name": "Default"
        }
    }
}` %}}

Exchange a username and password for a session token. The returned `token.id` is the bearer string used to authenticate subsequent Portal API requests.

This endpoint does not require authentication.

<b>Request Body</b>

The request body should be JSON-encoded.

- **username**: The user's username.
- **password**: The user's password.

<b>Response Schema</b>

On success, the endpoint returns the new session token and the authenticated user record.

- `token.id`: The bearer token string. Send this in the `Authorization` header on subsequent requests.
- `token.userId`: The ID of the user the token was issued to.
- `user.id`: The user's unique identifier.
- `user.email`: The user's email address.
- `user.isAdmin`: `true` if the user has administrator privileges on this OEM instance, otherwise `false`. Administrators have elevated privileges and have access to management endpoints under [Users & Team](/oem/portal-api-reference/).
- `user.isAccountOwner`: `true` if the user is the owner of the account, otherwise `false`.
- `user.account.id`: The ID of the account the user belongs to.
- `user.account.name`: The display name of the account.

<b>Error Responses</b>

- **400 Bad Request**: The request body is missing fields or is not valid JSON.
- **401 Unauthorized**: The username does not exist, or the password is incorrect.

{{% /apiEndpointCard %}}
