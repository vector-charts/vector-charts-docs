---
title: "Delete User"
weight: 5
menu:
  oem:
    parent: "portal_api_reference_admin"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/portal/v1/admin/deleteUser" title="Delete User" request=`POST https://<your-host>:9909/api/portal/v1/admin/deleteUser
Authorization: Bearer <token>
Content-Type: application/json

{
    "id": 7
}` response=`Status Code: 200 OK
Response Body:
{
    "deletedUserId": 7,
    "jobId": 31
}` %}}

Delete a user. A background job is enqueued to remove the user's data and record from the chart instance; the deletion completes asynchronously. Track the job through the [Jobs](/oem/portal-api-reference/jobs/) endpoints.

A user cannot be deleted if any of the following are true:

- The user is the caller (you cannot delete yourself).
- The user is an administrator.
- The user is the only user on their account.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token belonging to an administrator.

<b>Request Body</b>

The request body should be JSON-encoded.

- **id**: The `id` of the user to delete.

<b>Response Schema</b>

On success, the endpoint returns the identifiers of the deleted user and the cleanup job.

- `deletedUserId`: The `id` of the user that was deleted.
- `jobId`: The `id` of the background job performing instance-side cleanup of the user's data.

<b>Error Responses</b>

- **400 Bad Request**: The request body is malformed, or the user cannot be deleted (self, administrator, or the only user on the account).
- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **403 Forbidden**: The authenticated user is not an administrator.
- **404 Not Found**: No user exists with the given `id`.

{{% /apiEndpointCard %}}
