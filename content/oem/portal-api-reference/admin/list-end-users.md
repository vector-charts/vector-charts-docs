---
title: "List Account End Users"
weight: 14
menu:
  oem:
    parent: "portal_api_reference_admin"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/portal/v1/admin/accounts/{accountId}/endUsers" title="List End Users" request=`GET https://<your-host>:9909/api/portal/v1/admin/accounts/42/endUsers
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
{
    "accountZid": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "available": true,
    "removable": true,
    "labelable": true,
    "seats": [
        {
            "endUserId": "7c2e9b14-6a3d-4f1e-9c80-2b5d8e1a4f67",
            "userData": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
            "label": "Account default",
            "firstSeenAt": 1736942400000,
            "lastSeenAt": 1736946000000,
            "removedAt": null,
            "isDefault": true,
            "licenses": [
                {
                    "productCode": "example-enc",
                    "displayName": "Example ENC",
                    "paidThrough": "2027-01-15T00:00:00.000Z",
                    "renews": true,
                    "subscriptionStatus": "active"
                }
            ]
        }
    ]
}` %}}

List the end users registered on an account. Tokens are omitted. This is the administrator counterpart to [List End Users](/oem/portal-api-reference/end-users/list/).

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token belonging to an administrator.

<b>Path Parameters</b>

- **accountId**: The `id` of the account. Must be a positive integer.

<b>Response Schema</b>

The response matches [List End Users](/oem/portal-api-reference/end-users/list/). `seats` includes `endUserId`, `label`, `firstSeenAt`, `lastSeenAt`, `removedAt`, `isDefault`, and `licenses` (`productCode`, `displayName`, `paidThrough`, `renews`, `subscriptionStatus`). The token is omitted.

<b>Error Responses</b>

- **400 Bad Request**: `accountId` is missing or is not a positive integer.
- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **403 Forbidden**: The authenticated user is not an administrator.
- **404 Not Found**: No account exists with the given `accountId`.

{{% /apiEndpointCard %}}
