---
title: "Preview End User"
weight: 8
menu:
  oem:
    parent: "portal_api_reference_end_users"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/portal/v1/endUsers/preview" title="Preview End User" request=`POST https://<your-host>:9909/api/portal/v1/endUsers/preview
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

Quote the cost of adding one new seat. The body is an empty object, `{}`. Nothing is stored. `lines` lists yearly products that would newly bill. An empty `lines` array means the added seat does not change the bill. On Vector Charts Cloud, send this request to `https://cloud.vectorcharts.com/api/portal/v1/endUsers/preview`.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or personal access token for the account. Any role is accepted.

<b>Request Body</b>

Send an empty JSON object.

<b>Response Schema</b>

- `currency`: ISO currency code for the amounts.
- `nextBill.date`: Unix timestamp of the next bill.
- `lines`: Products that would be billed for the new seat.
    - `productCode`: Product identifier.
    - `displayName`: Product name.
    - `quantity`: Number of units, `1` for the new seat.
    - `unitAmount`: Price of one unit, as an integer in the smallest unit of `currency`.
    - `amount`: Line total, as an integer in the smallest unit of `currency`.
- `total`: Sum of `lines`, as an integer in the smallest unit of `currency`.

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **404 Not Found**: Seat preview is not available.
- **502 Bad Gateway**: The chart store could not be reached.

{{% /apiEndpointCard %}}
