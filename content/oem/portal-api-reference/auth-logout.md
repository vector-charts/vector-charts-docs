---
title: "Logout"
weight: 4
menu:
  oem:
    parent: "portal_api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/portal/v1/auth/logout" title="Logout" request=`POST https://<your-host>:9909/api/portal/v1/auth/logout
Authorization: Bearer <token>` response=`Status Code: 204 No Content` %}}

Invalidate the session token used for the request. After a successful logout, the token can no longer be used to authenticate further requests.

This endpoint only invalidates session tokens. API tokens are managed through the [API Tokens endpoints](/oem/portal-api-reference/) and are not affected by this request.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token.

<b>Response</b>

On success, the endpoint returns a `204 No Content` response with an empty body.

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.

{{% /apiEndpointCard %}}
