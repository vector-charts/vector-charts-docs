---
title: "Create User"
weight: 3
menu:
  oem:
    parent: "portal_api_reference_admin"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/portal/v1/admin/createUser" title="Create User" request=`POST https://<your-host>:9909/api/portal/v1/admin/createUser
Authorization: Bearer <token>
Content-Type: application/json

{
    "accountId": 42,
    "username": "example@zydromarine.com",
    "password": "a-strong-password"
}` response=`Status Code: 200 OK
Response Body:
{
    "user": {
        "id": 7,
        "accountId": 42,
        "email": "example@zydromarine.com",
        "isAdmin": false,
        "createdAt": 1736942400000
    },
    "initialToken": {
        "id": "299ce9bf4f244300a96f3926240f9c0d",
        "name": "Default",
        "userId": 7,
        "accountId": 42,
        "userEmail": "example@zydromarine.com",
        "createdAt": 1736942400000,
        "lastUsedAt": null,
        "restrictions": null
    }
}` %}}

Create a new user on an existing account. A default API token is minted for the new user as part of the same operation. If the user is created but the token cannot be minted, the user is rolled back and an error is returned.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token belonging to an administrator.

<b>Request Body</b>

The request body should be JSON-encoded.

- **accountId**: The `id` of the account the user will belong to. The account must already exist.
- **username**: The new user's login username, which is also used as their email address.
- **password**: The new user's password. Must be at least 4 characters.

<b>Response Schema</b>

On success, the endpoint returns the new user and its default API token.

- `user`: The newly created user record. See [Get User](/oem/portal-api-reference/admin/get-user/) for the field descriptions.
- `initialToken`: The default API token minted for the new user. The `id` field is the bearer string. See [Create API Token For User](/oem/portal-api-reference/admin/create-api-token/) for the full schema.

<b>Error Responses</b>

- **400 Bad Request**: The request body is missing required fields, or the `username` is already in use.
- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **403 Forbidden**: The authenticated user is not an administrator.
- **404 Not Found**: No account exists with the given `accountId`.

{{% /apiEndpointCard %}}
