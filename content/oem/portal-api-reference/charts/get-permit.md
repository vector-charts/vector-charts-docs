---
title: "Get S-63 Permit"
weight: 1
menu:
  oem:
    parent: "portal_api_reference_charts"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/portal/v1/charts/getPermit" title="Get S-63 Permit" request=`GET https://<your-host>:9909/api/portal/v1/charts/getPermit
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
{
    "permitId": "01234567ABCDEF0123456789ABCDEF01"
}` %}}

Return the S-63 user permit currently assigned to the account. The permit is the identifier you provide to a chart distributor when requesting encrypted S-63 charts. The distributor uses the permit to encrypt charts so that they can only be decrypted by your OEM instance.

If a chart distributor has issued you a `.prm` file, upload it through [Upload Chart](/oem/portal-api-reference/charts/upload/) to install the permit on the account.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token.

<b>Response Schema</b>

On success, the endpoint returns the permit assigned to the account.

- `permitId`: The S-63 user permit string.

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **404 Not Found**: No S-63 permit has been installed on the account.

{{% /apiEndpointCard %}}
