---
title: "Create Account"
weight: 9
menu:
  oem:
    parent: "portal_api_reference_admin"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/portal/v1/admin/createAccount" title="Create Account" request=`POST https://<your-host>:9909/api/portal/v1/admin/createAccount
Authorization: Bearer <token>
Content-Type: application/json

{
    "name": "Zydro Marine",
    "username": "owner@zydromarine.com",
    "password": "a-strong-password"
}` response=`Status Code: 200 OK
Response Body:
{
    "account": {
        "id": 42,
        "name": "Zydro Marine",
        "planInstance": "oem",
        "metadata": {},
        "createdAt": 1736942400000
    },
    "user": {
        "id": 7,
        "accountId": 42,
        "email": "owner@zydromarine.com",
        "isAdmin": false,
        "createdAt": 1736942400000
    },
    "initialToken": {
        "id": "299ce9bf4f244300a96f3926240f9c0d",
        "name": "Default",
        "userId": 7,
        "accountId": 42,
        "userEmail": "owner@zydromarine.com",
        "createdAt": 1736942400000,
        "lastUsedAt": null,
        "restrictions": null
    }
}` %}}

Create a new account together with its primary user and a default API token, in a single operation. The new account inherits the `planInstance` of the calling administrator's account, so it is bound to the same chart instance. If any step fails, the partially created account and user are rolled back.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token belonging to an administrator.

<b>Request Body</b>

The request body should be JSON-encoded.

- **name**: The human-readable name for the new account.
- **username**: The login username of the account's primary user, which is also used as their email address.
- **password**: The primary user's password. Must be at least 4 characters.

<b>Response Schema</b>

On success, the endpoint returns the new account, its primary user, and a default API token.

- `account`: The newly created account record. See [Get Account](/oem/portal-api-reference/admin/get-account/) for the field descriptions.
- `user`: The primary user created on the account. See [Get User](/oem/portal-api-reference/admin/get-user/) for the field descriptions.
- `initialToken`: The default API token minted for the primary user. The `id` field is the bearer string. See [Create API Token For User](/oem/portal-api-reference/admin/create-api-token/) for the full schema.

<b>Error Responses</b>

- **400 Bad Request**: The request body is missing required fields, or the `username` is already in use.
- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **403 Forbidden**: The authenticated user is not an administrator.

{{% /apiEndpointCard %}}
