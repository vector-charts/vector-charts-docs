---
title: "Edit Account"
weight: 10
menu:
  oem:
    parent: "portal_api_reference_admin"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/portal/v1/admin/editAccount" title="Edit Account" request=`POST https://<your-host>:9909/api/portal/v1/admin/editAccount
Authorization: Bearer <token>
Content-Type: application/json

{
    "id": 42,
    "name": "Acme Marine Ltd."
}` response=`Status Code: 200 OK
Response Body:
{
    "id": 42,
    "name": "Acme Marine Ltd.",
    "planInstance": "oem",
    "metadata": {},
    "createdAt": 1736942400000
}` %}}

Rename an account.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token belonging to an administrator.

<b>Request Body</b>

The request body should be JSON-encoded.

- **id**: The `id` of the account to edit.
- **name**: The new name for the account.

<b>Response Schema</b>

On success, the endpoint returns the updated account record. See [Get Account](/oem/portal-api-reference/admin/get-account/) for the field descriptions.

<b>Error Responses</b>

- **400 Bad Request**: The request body is missing the `id` or `name` field.
- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **403 Forbidden**: The authenticated user is not an administrator.
- **404 Not Found**: No account exists with the given `id`.

{{% /apiEndpointCard %}}
