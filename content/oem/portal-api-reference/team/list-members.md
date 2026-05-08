---
title: "List Team Members"
weight: 1
menu:
  oem:
    parent: "portal_api_reference_team"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/portal/v1/team/members" title="List Team Members" request=`GET https://<your-host>:9909/api/portal/v1/team/members
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
[
    {
        "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
        "email": "owner@example.com",
        "isAdmin": true,
        "createdAt": 1736942400000
    },
    {
        "id": "b2c3d4e5-f6a7-8901-bcde-f12345678901",
        "email": "operator@example.com",
        "isAdmin": false,
        "createdAt": 1737028800000
    }
]` %}}

List all users on the caller's account, ordered by creation time.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token.

<b>Response Schema</b>

The endpoint returns an array of user records.

- `id`: The unique identifier for the user.
- `email`: The user's email address.
- `isAdmin`: `true` if the user has administrator privileges on this OEM instance, otherwise `false`.
- `createdAt`: Timestamp when the user was created, in milliseconds since unix epoch.

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.

{{% /apiEndpointCard %}}
