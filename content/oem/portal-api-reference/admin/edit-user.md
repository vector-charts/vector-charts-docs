---
title: "Edit User"
weight: 4
menu:
  oem:
    parent: "portal_api_reference_admin"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/portal/v1/admin/editUser" title="Edit User" request=`POST https://<your-host>:9909/api/portal/v1/admin/editUser
Authorization: Bearer <token>
Content-Type: application/json

{
    "id": 7,
    "username": "new-email@zydromarine.com",
    "password": "a-new-password"
}` response=`Status Code: 200 OK
Response Body:
{
    "id": 7,
    "email": "new-email@zydromarine.com",
    "createdAt": 1736942400000,
    "modifiedAt": 1737023400000
}` %}}

Update a user's username and/or password. At least one of `username` or `password` must be supplied; fields that are omitted are left unchanged.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token belonging to an administrator.

<b>Request Body</b>

The request body should be JSON-encoded.

- **id**: The `id` of the user to edit.
- **username** (Optional): A new login username for the user. Must not already be in use by another user.
- **password** (Optional): A new password for the user. Must be at least 4 characters.

At least one of `username` or `password` is required.

<b>Response Schema</b>

On success, the endpoint returns the updated user record.

- `id`: The unique identifier for the user.
- `email`: The user's email address, reflecting the update.
- `createdAt`: Timestamp when the user was created, in milliseconds since unix epoch.
- `modifiedAt`: Timestamp when the user record was last modified, in milliseconds since unix epoch.

<b>Error Responses</b>

- **400 Bad Request**: The request body is malformed, neither `username` nor `password` was supplied, or the `username` is already in use.
- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **403 Forbidden**: The authenticated user is not an administrator.
- **404 Not Found**: No user exists with the given `id`.

{{% /apiEndpointCard %}}
