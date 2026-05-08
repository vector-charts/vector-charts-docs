---
title: "Delete Style"
weight: 5
menu:
  oem:
    parent: "portal_api_reference_styles"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-danger\">DELETE</div>"
---

{{% apiEndpointCard method="DELETE" path="/api/portal/v1/styles/{id}" title="Delete Style" request=`DELETE https://<your-host>:9909/api/portal/v1/styles/a1b2c3d4-e5f6-7890-abcd-ef1234567890
Authorization: Bearer <token>` response=`Status Code: 204 No Content` %}}

Permanently delete a style. Subsequent Core API requests that reference the deleted `styleId` will fall back to the default style.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token.

<b>Path Parameters</b>

- **id**: The `id` of the style to delete.

<b>Response</b>

On success, the endpoint returns a `204 No Content` response with an empty body.

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **404 Not Found**: No style exists with the given `id` on the caller's account.

{{% /apiEndpointCard %}}
