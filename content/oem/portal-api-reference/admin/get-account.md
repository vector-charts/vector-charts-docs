---
title: "Get Account"
weight: 8
menu:
  oem:
    parent: "portal_api_reference_admin"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/portal/v1/admin/getAccount" title="Get Account" request=`GET https://<your-host>:9909/api/portal/v1/admin/getAccount?id=42
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
{
    "id": 42,
    "name": "Zydro Marine",
    "planInstance": "oem",
    "metadata": {},
    "createdAt": 1736942400000
}` %}}

Return a single account by `id`.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token belonging to an administrator.

<b>Query Parameters</b>

- **id**: The `id` of the account to retrieve. Must be a positive integer.

<b>Response Schema</b>

The endpoint returns the account record. This is the same shape as an entry from [List Accounts](/oem/portal-api-reference/admin/list-accounts/).

- `id`: The unique identifier for the account.
- `name`: The human-readable account name.
- `planInstance`: The identifier of the chart instance the account is bound to, or `null` if unassigned.
- `metadata`: An object of arbitrary key-value metadata associated with the account.
- `createdAt`: Timestamp when the account was created, in milliseconds since unix epoch.

<b>Error Responses</b>

- **400 Bad Request**: The `id` query parameter is missing or is not a positive integer.
- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **403 Forbidden**: The authenticated user is not an administrator.
- **404 Not Found**: No account exists with the given `id`.

{{% /apiEndpointCard %}}
