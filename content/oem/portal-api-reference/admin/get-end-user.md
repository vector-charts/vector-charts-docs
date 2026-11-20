---
title: "Get Account End User"
weight: 15
menu:
  oem:
    parent: "portal_api_reference_admin"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/portal/v1/admin/accounts/{accountId}/endUsers/{endUserId}" title="Get End User" request=`GET https://<your-host>:9909/api/portal/v1/admin/accounts/42/endUsers/3f1a8c20-9b7e-4d62-8a15-6c0e4b2d9f71
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
{
    "endUserId": "3f1a8c20-9b7e-4d62-8a15-6c0e4b2d9f71",
    "label": "Harbor Pilot",
    "firstSeenAt": 1736943000000,
    "lastSeenAt": 1736947000000,
    "removedAt": null,
    "isDefault": false,
    "licenses": []
}` %}}

Return one end user on an account. The token is omitted. This is the administrator counterpart to [Get End User](/oem/portal-api-reference/end-users/get/).

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token belonging to an administrator.

<b>Path Parameters</b>

- **accountId**: The `id` of the account. Must be a positive integer.
- **endUserId**: Server-generated UUID of the end user.

<b>Response Schema</b>

The response is one seat from [List End Users](/oem/portal-api-reference/end-users/list/).

<b>Error Responses</b>

- **400 Bad Request**: `accountId` is not a positive integer, or `endUserId` is not a UUID.
- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **403 Forbidden**: The authenticated user is not an administrator.
- **404 Not Found**: No account exists with the given `accountId`, or no end user exists with that id on the account.
- **409 Conflict**: End users are not available on this instance.

{{% /apiEndpointCard %}}
