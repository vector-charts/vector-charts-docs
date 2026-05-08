---
title: "List All Accounts"
weight: 2
menu:
  oem:
    parent: "portal_api_reference_admin"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/portal/v1/admin/getAllAccounts" title="List All Accounts" request=`GET https://<your-host>:9909/api/portal/v1/admin/getAllAccounts
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
[
    {
        "id": "b2c3d4e5-f6a7-8901-bcde-f12345678901",
        "name": "Default"
    },
    {
        "id": "c3d4e5f6-a7b8-9012-cdef-123456789012",
        "name": "R&D"
    }
]` %}}

List all active accounts on the OEM instance.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header. **The user must have admin privileges**, indicated by `isAdmin: true` on the user record.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token belonging to an admin user.

<b>Response Schema</b>

The endpoint returns an array of account records.

- `id`: The unique identifier for the account.
- `name`: The display name of the account.

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing, the token is not valid, or the user does not have admin privileges.

{{% /apiEndpointCard %}}
