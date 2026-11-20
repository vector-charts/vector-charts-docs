---
title: "List End Users"
weight: 1
menu:
  oem:
    parent: "portal_api_reference_end_users"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/portal/v1/endUsers" title="List End Users" request=`GET https://<your-host>:9909/api/portal/v1/endUsers
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
            "label": "Default",
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
        },
        {
            "endUserId": "3f1a8c20-9b7e-4d62-8a15-6c0e4b2d9f71",
            "userData": "3f1a8c20-9b7e-4d62-8a15-6c0e4b2d9f71",
            "label": "Harbor Pilot",
            "firstSeenAt": 1736943000000,
            "lastSeenAt": 1736947000000,
            "removedAt": null,
            "isDefault": false,
            "licenses": []
        }
    ]
}` %}}

List the end users registered on the signed-in account. Tokens are omitted. On Vector Charts Cloud, send this request to `https://cloud.vectorcharts.com/api/portal/v1/endUsers`. An OEM instance administrator lists another account with [List Account End Users](/oem/portal-api-reference/admin/list-end-users/).

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token for the account.

<b>Response Schema</b>

- `accountZid`: The account's global identifier. `null` when the account has none.
- `available`: `true` when this instance can store end users. When `false`, `seats` is empty and creating a seat returns `409 Conflict`.
- `removable`: `true` when seats on this instance can be removed.
- `labelable`: `true` when seats on this instance store a label.
- `seats`: The registered end users, including the account default seat and seats that have been removed.

Each entry in `seats` has the following fields. The token is not one of them.

- `endUserId`: Server-generated UUID for the seat.
- `userData`: The account's global identifier on the default seat. On every other seat, the same value as `endUserId`.
- `label`: Display name. The default seat is `Default`. `null` when this instance does not store labels.
- `firstSeenAt`: Timestamp of the first chart request from this seat, in milliseconds since unix epoch. `null` if the seat has never been used.
- `lastSeenAt`: Timestamp of the most recent chart request from this seat, in milliseconds since unix epoch. `null` if the seat has never been used.
- `removedAt`: Timestamp when the seat was removed, in milliseconds since unix epoch. `null` while the seat is active.
- `isDefault`: `true` for the account default seat, which cannot be removed.
- `licenses`: Product terms for this seat. Empty when no terms are recorded for the account.
    - `productCode`: Product identifier.
    - `displayName`: Product name. Falls back to `productCode` when no display name is recorded.
    - `paidThrough`: ISO 8601 timestamp through which the product is paid, or `null`.
    - `renews`: `true` when the product renews.
    - `subscriptionStatus`: Subscription state for the product, or `null`.

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.

{{% /apiEndpointCard %}}
