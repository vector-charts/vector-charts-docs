---
title: "Create Style"
weight: 3
menu:
  oem:
    parent: "portal_api_reference_styles"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/portal/v1/styles" title="Create Style" request=`POST https://<your-host>:9909/api/portal/v1/styles
Authorization: Bearer <token>
Content-Type: application/json

{
    "name": "Vessel Map",
    "theme": "day"
}` response=`Status Code: 200 OK
Response Body:
{
    "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "name": "Vessel Map",
    "userEmail": "example@zydromarine.com",
    "createdAt": 1736942400000,
    "updatedAt": 1736942400000,
    "parameters": {
        "colors": { ... },
        "settings": {
            "iconSet": "enc-day",
            "soundingOpacity": 0.5,
            "showLightSectors": true
        }
    }
}` %}}

Create a new style. The new style is initialized with the default color palette and display settings for the chosen theme. To customize the style, follow up with a call to [Update Style](/oem/portal-api-reference/styles/update/).

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token.

<b>Request Body</b>

*The request body should be JSON-encoded.*

- **name**: A human-readable label for the style.
- **theme**: The base theme for the style. One of `day`, `dusk`, or `night`. See [Styles](/oem/portal-api-reference/styles/) for what each theme provides.

<b>Response Schema</b>

On success, the endpoint returns the newly created style record. The shape matches an entry from [List Styles](/oem/portal-api-reference/styles/list/).

<b>Error Responses</b>

- **400 Bad Request**: The `name` or `theme` field is missing.
- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.

{{% /apiEndpointCard %}}
