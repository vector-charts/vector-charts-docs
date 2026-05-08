---
title: "Create Job"
weight: 3
menu:
  oem:
    parent: "portal_api_reference_jobs"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/portal/v1/jobs" title="Create Job" request=`POST https://<your-host>:9909/api/portal/v1/jobs
Authorization: Bearer <token>
Content-Type: application/json

{
    "jobType": "refresh-public-charts"
}` response=`Status Code: 200 OK
Response Body:
{
    "jobId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "jobState": "pending"
}` %}}

Start a job on the OEM instance. The job runs asynchronously. Use [List Jobs](/oem/portal-api-reference/jobs/list/) to track its progress.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token.

<b>Request Body</b>

The request body should be JSON-encoded.

- **jobType**: The type of job to start. Must be one of the documented types listed in [Jobs](/oem/portal-api-reference/jobs/).

<b>Response Schema</b>

On success, the endpoint returns identifiers for the newly created job.

- `jobId`: The unique identifier of the new job. Use this to find the job in subsequent [List Jobs](/oem/portal-api-reference/jobs/list/) responses.
- `jobState`: The state of the new job. Always `pending` on a successful response.

<b>Error Responses</b>

- **400 Bad Request**: The `jobType` field is missing or is not one of the allowed values.
- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **409 Conflict**: A job of the requested `jobType` is already `pending` or `running` on the instance.

{{% /apiEndpointCard %}}
