---
title: "Remove Account End User"
weight: 20
menu:
  oem:
    parent: "portal_api_reference_admin"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-warning\">DELETE</div>"
---

{{% apiEndpointCard method="DELETE" path="/api/portal/v1/admin/accounts/{accountId}/endUsers/{endUserId}" title="Remove End User" request=`DELETE https://<your-host>:9909/api/portal/v1/admin/accounts/42/endUsers/3f1a8c20-9b7e-4d62-8a15-6c0e4b2d9f71
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
{
    "endUserId": "3f1a8c20-9b7e-4d62-8a15-6c0e4b2d9f71",
    "removed": true
}` %}}

Remove an end user and revoke its End User Token. The account default seat cannot be removed. This is the administrator counterpart to [Remove End User](/oem/portal-api-reference/end-users/delete/).

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token belonging to an administrator.

<b>Path Parameters</b>

- **accountId**: The `id` of the account. Must be a positive integer.
- **endUserId**: Server-generated UUID of the end user.

<b>Response Schema</b>

- `endUserId`: Server-generated UUID of the removed seat.
- `removed`: `true` when the seat was removed.

<b>Error Responses</b>

- **400 Bad Request**: `accountId` is not a positive integer, `endUserId` is not a UUID, or the seat is the account default seat.
- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **403 Forbidden**: The authenticated user is not an administrator.
- **404 Not Found**: No account exists with the given `accountId`, or no end user exists with that id on the account.
- **409 Conflict**: End users are not available on this instance, or this instance cannot remove seats yet.

{{% /apiEndpointCard %}}
