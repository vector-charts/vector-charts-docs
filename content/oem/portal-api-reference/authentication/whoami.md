---
title: "Get Authenticated User"
weight: 3
menu:
  oem:
    parent: "portal_api_reference_authentication"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/portal/v1/auth/whoami" title="Get Authenticated User" request=`GET https://<your-host>:9909/api/portal/v1/auth/whoami
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
{
    "id": 1,
    "email": "admin",
    "isAdmin": true,
    "isAccountOwner": false,
    "account": {
        "id": 1,
        "name": "Default"
    }
}` %}}

Return the user record associated with the bearer token used for the request. This is typically used by client applications to load the current user's profile after authenticating.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token.

<b>Response Schema</b>

The endpoint returns the authenticated user record.

- `id`: The user's unique identifier.
- `email`: The user's email address.
- `isAdmin`: `true` if the user has administrator privileges on this OEM instance, otherwise `false`. Administrators have elevated privileges and have access to management endpoints under [Users & Team](/oem/portal-api-reference/).
- `isAccountOwner`: `true` if the user is the owner of the account, otherwise `false`.
- `account.id`: The ID of the account the user belongs to.
- `account.name`: The display name of the account.

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.

{{% /apiEndpointCard %}}
