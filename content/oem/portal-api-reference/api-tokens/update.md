---
title: "Update API Token"
weight: 3
menu:
  oem:
    parent: "portal_api_reference_api_tokens"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/portal/v1/apiTokens/{id}" title="Update API Token" request=`POST https://<your-host>:9909/api/portal/v1/apiTokens/299ce9bf4f244300a96f3926240f9c0d
Authorization: Bearer <token>
Content-Type: application/json

{
    "restrictions": {
        "hosts": ["maps.example.com", "admin.example.com"]
    }
}` response=`Status Code: 200 OK
Response Body:
{
    "id": "299ce9bf4f244300a96f3926240f9c0d",
    "name": "Production Token",
    "userId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "userEmail": "example@zydromarine.com",
    "createdAt": 1736942400000,
    "lastUsedAt": 1736946000000,
    "restrictions": {
        "hosts": ["maps.example.com", "admin.example.com"]
    }
}` %}}

Update the name or restrictions of an existing API token. Only the fields included in the request body are modified. Fields that are omitted are left unchanged.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token.

<b>Path Parameters</b>

- **id**: The `id` of the token to update.

<b>Request Body</b>

*The request body should be JSON-encoded.*

- **name** (Optional): A human-readable label for the token.
- **restrictions** (Optional): An object describing limits on how the token can be used. See [Create API Token](/oem/portal-api-reference/api-tokens/create/) for the full schema.

<b>Response Schema</b>

On success, the endpoint returns the updated token record.

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **404 Not Found**: No token exists with the given `id` on the caller's account.

{{% /apiEndpointCard %}}
