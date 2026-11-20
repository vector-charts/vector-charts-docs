---
title: "Preview Account End User"
weight: 21
menu:
  oem:
    parent: "portal_api_reference_admin"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/portal/v1/admin/accounts/{accountId}/endUsers/preview" title="Preview End User" request=`POST https://<your-host>:9909/api/portal/v1/admin/accounts/42/endUsers/preview
Authorization: Bearer <token>
Content-Type: application/json

{}` response=`Status Code: 200 OK
Response Body:
{
    "currency": "usd",
    "nextBill": {
        "date": 1739520000
    },
    "lines": [
        {
            "productCode": "example-enc",
            "displayName": "Example ENC",
            "quantity": 1,
            "unitAmount": 12000,
            "amount": 12000
        }
    ],
    "total": 12000
}` %}}

Quote the cost of adding one new seat to an account. The body is an empty object, `{}`. Nothing is stored. This is the administrator counterpart to [Preview End User](/oem/portal-api-reference/end-users/preview/).

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token belonging to an administrator.

<b>Path Parameters</b>

- **accountId**: The `id` of the account. Must be a positive integer.

<b>Request Body</b>

Send an empty JSON object.

<b>Response Schema</b>

The response matches [Preview End User](/oem/portal-api-reference/end-users/preview/). `lines` lists yearly products that would newly bill. An empty `lines` array means the added seat does not change the bill.

<b>Error Responses</b>

- **400 Bad Request**: `accountId` is not a positive integer.
- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **403 Forbidden**: The authenticated user is not an administrator.
- **404 Not Found**: No account exists with the given `accountId`, or seat preview is not available.
- **502 Bad Gateway**: The chart store could not be reached.

{{% /apiEndpointCard %}}
