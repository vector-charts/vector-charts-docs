---
title: "List Users"
weight: 1
menu:
  oem:
    parent: "portal_api_reference_admin"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/portal/v1/admin/getAllUsers" title="List Users" request=`GET https://<your-host>:9909/api/portal/v1/admin/getAllUsers
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
[
    {
        "id": 1,
        "email": "admin",
        "accountId": 1,
        "isAdmin": true,
        "createdAt": 1736942400000
    },
    {
        "id": 7,
        "email": "example@zydromarine.com",
        "accountId": 42,
        "isAdmin": false,
        "createdAt": 1736942400000
    }
]` %}}

List every user across all accounts on the instance.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token belonging to an administrator.

<b>Response Schema</b>

The endpoint returns an array of user records.

- `id`: The unique identifier for the user.
- `email`: The user's email address, which doubles as their login username.
- `accountId`: The `id` of the account the user belongs to.
- `isAdmin`: `true` if the user has administrator privileges, otherwise `false`.
- `createdAt`: Timestamp when the user was created, in milliseconds since unix epoch.

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **403 Forbidden**: The authenticated user is not an administrator.

{{% /apiEndpointCard %}}
