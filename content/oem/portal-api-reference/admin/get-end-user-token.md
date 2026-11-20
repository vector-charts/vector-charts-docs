---
title: "Get Account End User Token"
weight: 17
menu:
  oem:
    parent: "portal_api_reference_admin"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/portal/v1/admin/accounts/{accountId}/endUsers/{endUserId}/token" title="Get End User Token" request=`GET https://<your-host>:9909/api/portal/v1/admin/accounts/42/endUsers/3f1a8c20-9b7e-4d62-8a15-6c0e4b2d9f71/token
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
{
    "endUserId": "3f1a8c20-9b7e-4d62-8a15-6c0e4b2d9f71",
    "token": "k7R2nQ8mV4pL0sYc3wHj6tB9uE1aZx5NfDg"
}` %}}

Return the End User Token for an active seat. This route is administrator-only. A removed seat has no token. This is the administrator counterpart to [Get End User Token](/oem/portal-api-reference/end-users/get-token/).

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token belonging to an administrator.

<b>Path Parameters</b>

- **accountId**: The `id` of the account. Must be a positive integer.
- **endUserId**: Server-generated UUID of the end user.

<b>Response Schema</b>

- `endUserId`: Server-generated UUID of the seat.
- `token`: The current End User Token.

<b>Error Responses</b>

- **400 Bad Request**: `accountId` is not a positive integer, or `endUserId` is not a UUID.
- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **403 Forbidden**: The authenticated user is not an administrator.
- **404 Not Found**: No account exists with the given `accountId`, or no end user exists with that id on the account.
- **409 Conflict**: The seat was removed and its token is revoked, or this instance cannot store End User Tokens yet.

{{% /apiEndpointCard %}}
