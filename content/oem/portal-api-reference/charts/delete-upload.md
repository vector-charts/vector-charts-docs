---
title: "Delete Upload"
weight: 5
menu:
  oem:
    parent: "portal_api_reference_charts"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-danger\">DELETE</div>"
---

{{% apiEndpointCard method="DELETE" path="/api/portal/v1/charts/uploads/{id}" title="Delete Upload" request=`DELETE https://<your-host>:9909/api/portal/v1/charts/uploads/a1b2c3d4-e5f6-7890-abcd-ef1234567890
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
{
    "message": "Upload deletion scheduled"
}` %}}

Schedule deletion of an upload and the chart cells it produced. Deletion is asynchronous: the endpoint returns immediately, and a background job removes the upload's data from storage and the chart database. The upload is hidden from [List Uploads](/oem/portal-api-reference/charts/list-uploads/) as soon as the request is accepted.

Any active ingestion jobs for the upload are cancelled.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token.

<b>Path Parameters</b>

- **id**: The `id` of the upload to delete.

<b>Response Schema</b>

- `message`: A description of the action taken. Either `"Upload deletion scheduled"` for a newly scheduled deletion, or `"Upload deletion already scheduled"` if a deletion was already pending.

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **404 Not Found**: No upload exists with the given `id` on the caller's account.

{{% /apiEndpointCard %}}
