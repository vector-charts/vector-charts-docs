---
title: "List All Users"
weight: 1
menu:
  oem:
    parent: "portal_api_reference_admin"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/portal/v1/admin/getAllUsers" title="List All Users" request=`GET https://<your-host>:9909/api/portal/v1/admin/getAllUsers
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
[
    {
        "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
        "email": "owner@example.com"
    },
    {
        "id": "b2c3d4e5-f6a7-8901-bcde-f12345678901",
        "email": "operator@example.com"
    }
]` %}}

List all active users on the OEM instance, across all accounts. Useful for instance-wide audits.

For listing users on a specific account (typically the caller's), use [List Team Members](/oem/portal-api-reference/team/list-members/) instead.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header. **The user must have admin privileges**, indicated by `isAdmin: true` on the user record.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token belonging to an admin user.

<b>Response Schema</b>

The endpoint returns an array of minimal user records.

- `id`: The unique identifier for the user.
- `email`: The user's email address.

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing, the token is not valid, or the user does not have admin privileges.

{{% /apiEndpointCard %}}
