---
title: "Create Account End User"
weight: 16
menu:
  oem:
    parent: "portal_api_reference_admin"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/portal/v1/admin/accounts/{accountId}/endUsers" title="Create End User" request=`POST https://<your-host>:9909/api/portal/v1/admin/accounts/42/endUsers
Authorization: Bearer <token>
Content-Type: application/json

{
    "label": "Harbor Pilot"
}` response=`Status Code: 201 Created
Response Body:
{
    "endUserId": "3f1a8c20-9b7e-4d62-8a15-6c0e4b2d9f71",
    "label": "Harbor Pilot",
    "created": true,
    "token": "k7R2nQ8mV4pL0sYc3wHj6tB9uE1aZx5NfDg"
}` %}}

Create an end user on an account. `label` is required. The server generates the UUID `endUserId` and returns a new End User Token. This is the administrator counterpart to [Create End User](/oem/portal-api-reference/end-users/create/).

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token belonging to an administrator.

<b>Path Parameters</b>

- **accountId**: The `id` of the account. Must be a positive integer.

<b>Request Body</b>

The request body should be JSON-encoded.

- **label**: Display name for the seat. A string of 1 to 256 characters. Leading and trailing whitespace is removed.
- **metadata** (Optional): An object of arbitrary key-value data stored with the seat.

<b>Response Schema</b>

On success, the endpoint returns the new seat id, the stored label, `created: true`, and the new `token`. See [Create End User](/oem/portal-api-reference/end-users/create/) for the field descriptions.

<b>Error Responses</b>

- **400 Bad Request**: `accountId` is not a positive integer, `label` is missing, blank, or longer than 256 characters, or `metadata` is not an object.
- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **403 Forbidden**: The authenticated user is not an administrator.
- **404 Not Found**: No account exists with the given `accountId`.
- **409 Conflict**: End users are not available on this instance, or this instance cannot store a label or an End User Token yet.

{{% /apiEndpointCard %}}
