---
title: "List API Tokens"
weight: 1
menu:
  oem:
    parent: "portal_api_reference_api_tokens"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/portal/v1/apiTokens" title="List API Tokens" request=`GET https://<your-host>:9909/api/portal/v1/apiTokens
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
[
    {
        "id": "299ce9bf4f244300a96f3926240f9c0d",
        "name": "Development Token",
        "userId": 1,
        "userEmail": "example@zydromarine.com",
        "createdAt": 1736942400000,
        "lastUsedAt": 1736946000000,
        "restrictions": {
            "hosts": ["example.com"]
        }
    },
    {
        "id": "5f8e7d6c5b4a3210fedcba9876543210",
        "name": "Production Token",
        "userId": 1,
        "userEmail": "example@zydromarine.com",
        "createdAt": 1736942400000,
        "lastUsedAt": 1736946000000,
        "restrictions": null
    }
]` %}}

List all API tokens visible to the authenticated user. The response includes tokens that the user created, as well as tokens created by other users within the same account.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token.

<b>Response Schema</b>

The endpoint returns an array of API token records.

- `id`: The bearer token string. Used to authenticate Core API and Portal API requests.
- `name`: A human-readable label for the token.
- `userId`: The ID of the user who created the token.
- `userEmail`: The email of the user who created the token.
- `createdAt`: Timestamp when the token was created, in milliseconds since unix epoch.
- `lastUsedAt`: Timestamp of the most recent request authenticated by this token, in milliseconds since unix epoch. `null` if the token has never been used.
- `restrictions`: An object describing limits on how the token can be used, or `null` if unrestricted. See [Create API Token](/oem/portal-api-reference/api-tokens/create/) for the full schema.

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.

{{% /apiEndpointCard %}}
