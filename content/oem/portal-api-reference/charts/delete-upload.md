---
title: "Delete Upload"
weight: 5
menu:
  oem:
    parent: "portal_api_reference_charts"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-danger\">DELETE</div>"
---

{{% apiEndpointCard method="DELETE" path="/api/portal/v1/charts/uploads/{id}" title="Delete Upload" request=`DELETE https://<your-host>:9909/api/portal/v1/charts/uploads/5
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
{
    "message": "Upload deletion scheduled"
}` %}}

Delete an uploaded file and its associated chart data. Cancels any active ingestion jobs for that upload.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token.

<b>Path Parameters</b>

- **id**: The `id` of the upload to delete.

<b>Response Schema</b>

- `message`: A status message.

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **404 Not Found**: No upload exists with the given `id` on the caller's account.

{{% /apiEndpointCard %}}
