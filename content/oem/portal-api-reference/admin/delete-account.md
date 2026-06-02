---
title: "Delete Account"
weight: 11
menu:
  oem:
    parent: "portal_api_reference_admin"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/portal/v1/admin/deleteAccount" title="Delete Account" request=`POST https://<your-host>:9909/api/portal/v1/admin/deleteAccount
Authorization: Bearer <token>
Content-Type: application/json

{
    "id": 42
}` response=`Status Code: 200 OK
Response Body:
{
    "jobId": "5e37b9c1-a4c2-4b8e-9f3a-72d3f4a5b8e1"
}` %}}

Delete an account. A background job is enqueued to remove the account, all of its users, and their data from the chart instance; the deletion completes asynchronously. Track the job through the [Jobs](/oem/portal-api-reference/jobs/) endpoints.

An administrator cannot delete their own account.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token belonging to an administrator.

<b>Request Body</b>

The request body should be JSON-encoded.

- **id**: The `id` of the account to delete.

<b>Response Schema</b>

On success, the endpoint returns the identifier of the cleanup job.

- `jobId`: The `id` of the background job performing instance-side cleanup of the account's data.

<b>Error Responses</b>

- **400 Bad Request**: The request body is malformed, or the account is the caller's own account.
- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **403 Forbidden**: The authenticated user is not an administrator.
- **404 Not Found**: No account exists with the given `id`.

{{% /apiEndpointCard %}}
