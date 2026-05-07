---
title: "Invite Team Member"
weight: 2
menu:
  oem:
    parent: "portal_api_reference_team"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/portal/v1/team/invite" title="Invite Team Member" request=`POST https://<your-host>:9909/api/portal/v1/team/invite
Authorization: Bearer <token>
Content-Type: application/json

{
    "email": "newuser@example.com"
}` response=`Status Code: 204 No Content` %}}

Invite a new user to the caller's account. The invitee receives an email with a link to set their password and complete onboarding. Once they finish, they appear in the [List Team Members](/oem/portal-api-reference/team/list-members/) response with the same `accountId` as the inviter.

This endpoint requires a working SMTP configuration on the OEM instance. If email delivery is not configured, the invitation is recorded but the invitee will not receive a link.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token.

<b>Request Body</b>

The request body should be JSON-encoded.

- **email**: The email address of the user to invite. Must be a valid email format.

<b>Response</b>

On success, the endpoint returns a `204 No Content` response with an empty body.

<b>Error Responses</b>

- **400 Bad Request**: The `email` field is missing or is not a valid email format.
- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.

{{% /apiEndpointCard %}}
