---
title: "List Jobs"
weight: 2
menu:
  oem:
    parent: "portal_api_reference_jobs"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/portal/v1/jobs" title="List Jobs" request=`GET https://<your-host>:9909/api/portal/v1/jobs?activeOnly=true&limit=25&offset=0
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
{
    "jobs": [
        {
            "id": "5e37b9c1-a4c2-4b8e-9f3a-72d3f4a5b8e1",
            "parentJobId": null,
            "jobType": "refresh-public-charts",
            "jobState": "completed",
            "accountId": null,
            "parameters": {},
            "result": null,
            "logs": [],
            "percentComplete": 100,
            "priority": 0,
            "createdAt": 1736942400000,
            "updatedAt": 1736946000000,
            "steps": [
                {
                    "id": "f1a2b3c4-d5e6-7890-abcd-ef1234567890",
                    "jobId": "5e37b9c1-a4c2-4b8e-9f3a-72d3f4a5b8e1",
                    "stepName": "step_download_noaa",
                    "status": "completed",
                    "startedAt": 1736942410000,
                    "completedAt": 1736943100000,
                    "result": null,
                    "error": null,
                    "attempt": 1
                },
                {
                    "id": "8f3c2a1b-d4e5-6f78-90ab-cdef12345678",
                    "jobId": "5e37b9c1-a4c2-4b8e-9f3a-72d3f4a5b8e1",
                    "stepName": "step_index_noaa",
                    "status": "completed",
                    "startedAt": 1736943200000,
                    "completedAt": 1736945800000,
                    "result": null,
                    "error": null,
                    "attempt": 1
                }
            ]
        }
    ],
    "pagination": {
        "limit": 25,
        "offset": 0,
        "total": 1
    }
}` %}}

List jobs running on the instance, ordered most recent first. Each job record includes its current state, progress, logs, and any sub-task steps.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token.

<b>Query Parameters</b>

- **activeOnly** (Optional): If `true`, return only jobs in the `pending` or `running` state. Defaults to `false`.
- **limit** (Optional): Maximum number of jobs to return. Defaults to `25`. Capped at `200`.
- **offset** (Optional): Number of jobs to skip from the start of the list. Defaults to `0`. Combine with `limit` to page through results.

<b>Response Schema</b>

The endpoint returns a paginated list of job records, ordered most recent first.

- `jobs`: An array of job records.
- `jobs[].id`: The unique identifier for the job.
- `jobs[].parentJobId`: The `id` of the job that spawned this one, or `null` for jobs that have no parent. Used to model job trees (for example, an upload job spawning ingestion jobs).
- `jobs[].jobType`: The type of work being performed. See [Jobs](/oem/portal-api-reference/jobs/) for the documented types.
- `jobs[].jobState`: The current state of the job. See [Jobs](/oem/portal-api-reference/jobs/) for the lifecycle.
- `jobs[].accountId`: The ID of the account that owns the job, or `null` for system-wide maintenance jobs.
- `jobs[].parameters`: An object of inputs specific to the job type. The shape depends on the value of `jobType`.
- `jobs[].result`: An object of outputs produced when the job completes. `null` until the job reaches a terminal state. The shape depends on the value of `jobType`.
- `jobs[].logs`: An array of log entries emitted by the job. Each entry has `timestamp` (ISO 8601 UTC string), `type` (one of `info`, `warning`, `error`), and `message`.
- `jobs[].percentComplete`: An integer between `0` and `100` indicating the job's progress.
- `jobs[].priority`: An integer indicating the job's scheduling priority. Higher values run before lower values. Defaults to `0`.
- `jobs[].createdAt`: Timestamp when the job was created, in milliseconds since unix epoch.
- `jobs[].updatedAt`: Timestamp when the job was last updated, in milliseconds since unix epoch.
- `jobs[].steps`: An array of sub-task records belonging to the job. The shape of a step record is not part of the stable public surface.
- `pagination.limit`: The `limit` value applied to the request.
- `pagination.offset`: The `offset` value applied to the request.
- `pagination.total`: The total number of jobs matching the filter, across all pages.

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.

{{% /apiEndpointCard %}}
