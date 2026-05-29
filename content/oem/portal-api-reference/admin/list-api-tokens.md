---
title: "List Account API Tokens"
weight: 12
menu:
  oem:
    parent: "portal_api_reference_admin"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/portal/v1/admin/getApiTokens" title="List Account API Tokens" request=`GET https://<your-host>:9909/api/portal/v1/admin/getApiTokens?accountId=42
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
[
    {
        "id": "299ce9bf4f244300a96f3926240f9c0d",
        "name": "Default",
        "userId": 7,
        "accountId": 42,
        "userEmail": "example@zydromarine.com",
        "createdAt": 1736942400000,
        "lastUsedAt": 1736946000000,
        "restrictions": null
    }
]` %}}

List every API token belonging to a given account, across all of the account's users. This is the administrator counterpart to [List API Tokens](/oem/portal-api-reference/api-tokens/list/), which is scoped to the caller's own account.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token belonging to an administrator.

<b>Query Parameters</b>

- **accountId**: The `id` of the account whose tokens to list. Must be a positive integer.

<b>Response Schema</b>

The endpoint returns an array of API token records.

- `id`: The bearer token string. Used to authenticate Core API and Portal API requests.
- `name`: A human-readable label for the token.
- `userId`: The `id` of the user the token belongs to.
- `accountId`: The `id` of the account the token belongs to.
- `userEmail`: The email of the user the token belongs to.
- `createdAt`: Timestamp when the token was created, in milliseconds since unix epoch.
- `lastUsedAt`: Timestamp of the most recent request authenticated by this token, in milliseconds since unix epoch. `null` if the token has never been used.
- `restrictions`: An object describing limits on how the token can be used, or `null` if unrestricted. See [Create API Token For User](/oem/portal-api-reference/admin/create-api-token/) for the full schema.

<b>Error Responses</b>

- **400 Bad Request**: The `accountId` query parameter is missing or is not a positive integer.
- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **403 Forbidden**: The authenticated user is not an administrator.
- **404 Not Found**: No account exists with the given `accountId`.

{{% /apiEndpointCard %}}
