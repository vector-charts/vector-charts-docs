---
title: "Get Jobs"
weight: 7
menu:
  main:
    parent: "api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/v1/jobs" title="Get Jobs" request=`GET https://api.vectorcharts.com/api/v1/jobs
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
[
    {
        "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
        "job_type": "refresh-public-charts",
        "job_state": "completed",
        "parameters": null,
        "percent_complete": 100,
        "created_at": 1736942400000,
        "updated_at": 1736946000000
    },
    {
        "id": "b2c3d4e5-f6a7-8901-bcde-f12345678901",
        "job_type": "index-custom-encs",
        "job_state": "processing",
        "parameters": null,
        "percent_complete": 45,
        "created_at": 1736950000000,
        "updated_at": 1736950500000
    }
]` %}}

<span style="color:#9e6c2e">Enterprise Only: This endpoint is only available on enterprise instances.

Retrieve all jobs on the instance, sorted by most recently updated first. This can be used to monitor the status of internal operations.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization** <span style="color:red;">(Required)</span>: `Bearer <token>` — a valid Vector Charts API token.

<b>Response Schema</b>

The endpoint returns an array of job objects. Each job has the following fields:

- `id`: Unique identifier for the job.
- `job_type`: The type of job (e.g. `"refresh-public-charts"`, `"index-custom-encs"`).
- `job_state`: Current state of the job: `"pending"`, `"processing"`, `"completed"`, or `"failed"`.
- `parameters`: Job-specific parameters, if any.
- `percent_complete`: Progress indicator (0–100).
- `created_at`: Timestamp when the job was created, in milliseconds since unix epoch.
- `updated_at`: Timestamp when the job was last updated, in milliseconds since unix epoch.

{{% /apiEndpointCard %}}