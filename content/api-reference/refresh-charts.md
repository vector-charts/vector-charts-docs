---
title: "Refresh Public Charts"
weight: 6
menu:
  main:
    parent: "api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/v1/charts/refresh" title="Refresh Public Charts" request=`POST https://api.vectorcharts.com/api/v1/charts/refresh
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
{
    "job_id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "job_state": "pending"
}` %}}

<span style="color:#9e6c2e">Enterprise Only: This endpoint is only available on enterprise instances.

Trigger a refresh of all public nautical chart data (NOAA ENCs and USA Inland ENCs). This creates an asynchronous background job that downloads the latest charts from their upstream sources and re-indexes them into the Vector Charts system.

Only one refresh job can run at a time. If a refresh is already in progress, the endpoint will return a `409 Conflict` error.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization** <span style="color:red;">(Required)</span>: `Bearer <token>` — a valid Vector Charts API token.

<b>Request Body</b>

This endpoint does not accept a request body.

<b>Response Schema</b>

On success, the endpoint returns a response indicating that the job has been queued for processing:

- `job_id`: Unique identifier for the chart refresh job.
- `job_state`: Initial status will be `"pending"`. Transitions to `"processing"`, then `"completed"` or `"failed"`.

<b>Error Responses</b>

- **403 Forbidden**: The instance is not an enterprise deployment.
- **409 Conflict**: A chart refresh job is already in progress.

{{% /apiEndpointCard %}}