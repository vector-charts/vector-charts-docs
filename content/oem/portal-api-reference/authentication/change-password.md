---
title: "Change Password"
weight: 4
menu:
  oem:
    parent: "portal_api_reference_authentication"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/portal/v1/user/passwordChange" title="Change Password" request=`POST https://<your-host>:9909/api/portal/v1/user/passwordChange
Authorization: Bearer <token>
Content-Type: application/json

{
    "password": "new-strong-password"
}` response=`Status Code: 204 No Content` %}}

Change the password of the user associated with the bearer token used for the request. Existing session tokens for the user remain valid until they are explicitly invalidated through the [logout endpoint](/oem/portal-api-reference/authentication/logout/).

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token.

<b>Request Body</b>

The request body should be JSON-encoded.

- **password**: The new password. Must be at least 4 characters long.

<b>Response</b>

On success, the endpoint returns a `204 No Content` response with an empty body.

<b>Error Responses</b>

- **400 Bad Request**: The `password` field is missing, or the supplied password is too short.
- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.

{{% /apiEndpointCard %}}
