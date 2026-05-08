---
title: "Create API Token"
weight: 2
menu:
  oem:
    parent: "portal_api_reference_api_tokens"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/portal/v1/apiTokens" title="Create API Token" request=`POST https://<your-host>:9909/api/portal/v1/apiTokens
Authorization: Bearer <token>
Content-Type: application/json

{
    "name": "Production Token",
    "restrictions": {
        "hosts": ["example.com"]
    }
}` response=`Status Code: 200 OK
Response Body:
{
    "id": "299ce9bf4f244300a96f3926240f9c0d",
    "name": "Production Token",
    "userId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "userEmail": "example@zydromarine.com",
    "createdAt": 1736942400000,
    "lastUsedAt": null,
    "restrictions": {
        "hosts": ["example.com"]
    }
}` %}}

Create a new API token. The `id` field of the returned token is the bearer string.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token.

<b>Request Body</b>

The request body should be JSON-encoded.

- **name**: A human-readable label for the token. Used in the admin UI to distinguish tokens.
- **restrictions** (Optional): An object describing limits on how the token can be used.

<b>Restrictions</b>

The `restrictions` object accepts the following fields:

- **hosts**: An array of hostnames the token is allowed to be used from. The hostname is matched exactly against the `Origin` header of incoming requests.

<b>Response Schema</b>

On success, the endpoint returns the newly created token record. The shape matches an entry from [List API Tokens](/oem/portal-api-reference/api-tokens/list/).

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.

{{% /apiEndpointCard %}}
