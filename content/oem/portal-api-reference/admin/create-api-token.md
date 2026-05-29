---
title: "Create API Token For User"
weight: 13
menu:
  oem:
    parent: "portal_api_reference_admin"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/portal/v1/admin/createApiToken" title="Create API Token For User" request=`POST https://<your-host>:9909/api/portal/v1/admin/createApiToken
Authorization: Bearer <token>
Content-Type: application/json

{
    "userId": 7,
    "accountId": 42,
    "name": "Production Token",
    "restrictions": {
        "hosts": ["example.com"]
    }
}` response=`Status Code: 200 OK
Response Body:
{
    "id": "5f8e7d6c5b4a3210fedcba9876543210",
    "name": "Production Token",
    "userId": 7,
    "accountId": 42,
    "userEmail": "example@zydromarine.com",
    "createdAt": 1736942400000,
    "lastUsedAt": null,
    "restrictions": {
        "hosts": ["example.com"]
    }
}` %}}

Mint an API token for a specific user on a specific account. This is the administrator counterpart to [Create API Token](/oem/portal-api-reference/api-tokens/create/), which always creates the token for the calling user. The `id` field of the returned token is the bearer string.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token belonging to an administrator.

<b>Request Body</b>

The request body should be JSON-encoded.

- **userId**: The `id` of the user the token will belong to. The user must belong to `accountId`.
- **accountId**: The `id` of the account the token will belong to.
- **name**: A human-readable label for the token. Used in the admin UI to distinguish tokens.
- **restrictions** (Optional): An object describing limits on how the token can be used.

<b>Restrictions</b>

The `restrictions` object accepts the following fields:

- **hosts**: An array of hostnames the token is allowed to be used from. The hostname is matched exactly against the `Origin` header of incoming requests.

<b>Response Schema</b>

On success, the endpoint returns the newly created token record. The shape matches an entry from [List Account API Tokens](/oem/portal-api-reference/admin/list-api-tokens/).

<b>Error Responses</b>

- **400 Bad Request**: The request body is malformed, or the user does not belong to the specified account.
- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **403 Forbidden**: The authenticated user is not an administrator.
- **404 Not Found**: No user or account exists with the given identifiers.

{{% /apiEndpointCard %}}
