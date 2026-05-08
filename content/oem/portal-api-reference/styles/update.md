---
title: "Update Style"
weight: 4
menu:
  oem:
    parent: "portal_api_reference_styles"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/portal/v1/styles/{id}" title="Update Style" request=`POST https://<your-host>:9909/api/portal/v1/styles/a1b2c3d4-e5f6-7890-abcd-ef1234567890
Authorization: Bearer <token>
Content-Type: application/json

{
    "parameters": {
        "colors": { ... },
        "settings": {
            "iconSet": "enc-day",
            "soundingOpacity": 0.7,
            "showLightSectors": false
        }
    }
}` response=`Status Code: 200 OK
Response Body:
{
    "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "name": "Vessel Map",
    "userEmail": "example@zydromarine.com",
    "createdAt": 1736942400000,
    "updatedAt": 1736950000000,
    "parameters": {
        "colors": { ... },
        "settings": {
            "iconSet": "enc-day",
            "soundingOpacity": 0.7,
            "showLightSectors": false
        }
    }
}` %}}

Update the name or rendering parameters of an existing style. Only the fields included in the request body are modified. Fields that are omitted are left unchanged.

Updates take effect immediately for any subsequent Core API request that references the style by ID.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token.

<b>Path Parameters</b>

- **id**: The `id` of the style to update.

<b>Request Body</b>

The request body should be JSON-encoded.

- **name** (Optional): A human-readable label for the style.
- **parameters** (Optional): The full rendering parameters object. See [Styles](/oem/portal-api-reference/styles/) for the schema.

<b>Response Schema</b>

On success, the endpoint returns the updated style record. The shape matches an entry from [List Styles](/oem/portal-api-reference/styles/list/).

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **404 Not Found**: No style exists with the given `id` on the caller's account.

{{% /apiEndpointCard %}}
