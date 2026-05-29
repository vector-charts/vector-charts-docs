---
title: "Get User"
weight: 2
menu:
  oem:
    parent: "portal_api_reference_admin"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/portal/v1/admin/getUser" title="Get User" request=`GET https://<your-host>:9909/api/portal/v1/admin/getUser?id=7
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
{
    "id": 7,
    "accountId": 42,
    "email": "example@zydromarine.com",
    "isAdmin": false,
    "createdAt": 1736942400000,
    "modifiedAt": 1736942400000
}` %}}

Return a single user by `id`, from any account on the instance.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token belonging to an administrator.

<b>Query Parameters</b>

- **id**: The `id` of the user to retrieve. Must be a positive integer.

<b>Response Schema</b>

The endpoint returns a single user record.

- `id`: The unique identifier for the user.
- `accountId`: The `id` of the account the user belongs to.
- `email`: The user's email address, which doubles as their login username.
- `isAdmin`: `true` if the user has administrator privileges, otherwise `false`.
- `createdAt`: Timestamp when the user was created, in milliseconds since unix epoch.
- `modifiedAt`: Timestamp when the user record was last modified, in milliseconds since unix epoch.

<b>Error Responses</b>

- **400 Bad Request**: The `id` query parameter is missing or is not a positive integer.
- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **403 Forbidden**: The authenticated user is not an administrator.
- **404 Not Found**: No user exists with the given `id`.

{{% /apiEndpointCard %}}
