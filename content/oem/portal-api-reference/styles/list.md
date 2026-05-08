---
title: "List Styles"
weight: 1
menu:
  oem:
    parent: "portal_api_reference_styles"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/portal/v1/styles" title="List Styles" request=`GET https://<your-host>:9909/api/portal/v1/styles
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
[
    {
        "id": 42,
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
    }
]` %}}

List all styles on the account, ordered most recent first.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token.

<b>Response Schema</b>

The endpoint returns an array of style records.

- `id`: The unique identifier for the style. Use this in the Core API as `?styleId=<id>` to render with this style.
- `name`: The display name of the style.
- `userEmail`: The email of the user who created the style.
- `createdAt`: Timestamp when the style was created, in milliseconds since unix epoch.
- `updatedAt`: Timestamp when the style was last modified, in milliseconds since unix epoch.
- `parameters`: The rendering parameters for the style. See [Styles](/oem/portal-api-reference/styles/) for the schema.

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.

{{% /apiEndpointCard %}}
