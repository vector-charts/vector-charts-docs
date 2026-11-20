---
title: "Create End User"
weight: 3
menu:
  oem:
    parent: "portal_api_reference_end_users"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/portal/v1/endUsers" title="Create End User" request=`POST https://<your-host>:9909/api/portal/v1/endUsers
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

Create an end user on the signed-in account. `label` is required. The server generates the UUID `endUserId` and returns a new End User Token. Store the token: list and get responses do not include it. On Vector Charts Cloud, send this request to `https://cloud.vectorcharts.com/api/portal/v1/endUsers`. An OEM instance administrator creates a seat on another account with [Create Account End User](/oem/portal-api-reference/admin/create-end-user/).

Quote the price of one new seat before creating it with [Preview End User](/oem/portal-api-reference/end-users/preview/).

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token for an account administrator.

<b>Request Body</b>

The request body should be JSON-encoded.

- **label**: Display name for the seat. A string of 1 to 256 characters. Leading and trailing whitespace is removed.
- **metadata** (Optional): An object of arbitrary key-value data stored with the seat.

<b>Response Schema</b>

- `endUserId`: Server-generated UUID for the new seat.
- `label`: The stored label.
- `created`: `true` when the seat was created.
- `token`: The End User Token. Send it as `Authorization: Bearer <token>` or the `token` query parameter on chart and tile requests. Present when this instance stores End User Tokens.

<b>Error Responses</b>

- **400 Bad Request**: `label` is missing, blank, or longer than 256 characters, or `metadata` is not an object.
- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **403 Forbidden**: The authenticated user is not an account administrator.
- **409 Conflict**: End users are not available on this instance, or this instance cannot store a label or an End User Token yet.

{{% /apiEndpointCard %}}
