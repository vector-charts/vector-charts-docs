---
title: "List Accounts"
weight: 7
menu:
  oem:
    parent: "portal_api_reference_admin"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/portal/v1/admin/getAllAccounts" title="List Accounts" request=`GET https://<your-host>:9909/api/portal/v1/admin/getAllAccounts
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
[
    {
        "id": 1,
        "name": "Default",
        "planInstance": "oem",
        "metadata": {},
        "createdAt": 1736942400000
    },
    {
        "id": 42,
        "name": "Zydro Marine",
        "planInstance": "oem",
        "metadata": {},
        "createdAt": 1736942400000
    }
]` %}}

List every account on the instance.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A personal access token (PAT) belonging to an administrator is required. A portal session token is also accepted. Tile API tokens are not.

<b>Response Schema</b>

The endpoint returns an array of account records.

- `id`: The unique identifier for the account.
- `name`: The human-readable account name.
- `planInstance`: The identifier of the chart instance the account is bound to, or `null` if unassigned.
- `metadata`: An object of arbitrary key-value metadata associated with the account.
- `createdAt`: Timestamp when the account was created, in milliseconds since unix epoch.

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **403 Forbidden**: The caller used a tile API token, or the authenticated user is not an administrator. A personal access token (PAT) is required.

{{% /apiEndpointCard %}}
