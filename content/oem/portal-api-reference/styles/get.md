---
title: "Get Style"
weight: 2
menu:
  oem:
    parent: "portal_api_reference_styles"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/portal/v1/styles/{id}" title="Get Style" request=`GET https://<your-host>:9909/api/portal/v1/styles/a1b2c3d4-e5f6-7890-abcd-ef1234567890
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
{
    "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "name": "Vessel Map",
    "userEmail": "example@zydromarine.com",
    "createdAt": 1736942400000,
    "updatedAt": 1736946000000,
    "parameters": {
        "colors": { ... },
        "settings": {
            "iconSet": "enc-day",
            "soundingOpacity": 0.5,
            "showLightSectors": true
        }
    }
}` %}}

Return the style with the given `id`. The style must belong to the caller's account.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token.

<b>Path Parameters</b>

- **id**: The `id` of the style to retrieve.

<b>Response Schema</b>

The endpoint returns a single style record. The shape matches an entry from [List Styles](/oem/portal-api-reference/styles/list/).

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **404 Not Found**: No style exists with the given `id` on the caller's account.

{{% /apiEndpointCard %}}
