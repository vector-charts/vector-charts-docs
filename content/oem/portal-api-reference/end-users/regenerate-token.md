---
title: "Regenerate End User Token"
weight: 5
menu:
  oem:
    parent: "portal_api_reference_end_users"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/portal/v1/endUsers/{endUserId}/token" title="Regenerate End User Token" request=`POST https://<your-host>:9909/api/portal/v1/endUsers/3f1a8c20-9b7e-4d62-8a15-6c0e4b2d9f71/token
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
{
    "endUserId": "3f1a8c20-9b7e-4d62-8a15-6c0e4b2d9f71",
    "token": "p9Lm4Qx2Va8Nc1Ws6Ht0Yb3Ke7Rf5UdJgZ"
}` %}}

Issue a new End User Token for an active seat. The previous token stops working. The request body is empty. On Vector Charts Cloud, send this request to `https://cloud.vectorcharts.com/api/portal/v1/endUsers/{endUserId}/token`. An OEM instance administrator regenerates a token on another account with [Regenerate Account End User Token](/oem/portal-api-reference/admin/regenerate-end-user-token/).

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or personal access token for the account. Any role is accepted.

<b>Path Parameters</b>

- **endUserId**: Server-generated UUID of the end user.

<b>Response Schema</b>

- `endUserId`: Server-generated UUID of the seat.
- `token`: The new End User Token.

<b>Error Responses</b>

- **400 Bad Request**: `endUserId` is not a UUID.
- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **404 Not Found**: No active end user exists with that id on the account.
- **409 Conflict**: This instance cannot issue End User Tokens yet.

{{% /apiEndpointCard %}}
