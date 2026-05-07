---
title: "Delete API Token"
weight: 4
menu:
  oem:
    parent: "portal_api_reference_api_tokens"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-danger\">DELETE</div>"
---

{{% apiEndpointCard method="DELETE" path="/api/portal/v1/apiTokens/{id}" title="Delete API Token" request=`DELETE https://<your-host>:9909/api/portal/v1/apiTokens/299ce9bf4f244300a96f3926240f9c0d
Authorization: Bearer <token>` response=`Status Code: 204 No Content` %}}

Permanently delete an API token. Any client using the deleted token will receive `401 Unauthorized` on subsequent requests.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token.

<b>Path Parameters</b>

- **id**: The `id` of the token to delete.

<b>Response</b>

On success, the endpoint returns a `204 No Content` response with an empty body.

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.

{{% /apiEndpointCard %}}
