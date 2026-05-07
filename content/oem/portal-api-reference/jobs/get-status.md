---
title: "Get Job Status"
weight: 1
menu:
  oem:
    parent: "portal_api_reference_jobs"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/portal/v1/jobs/getJobStatus" title="Get Job Status" request=`GET https://<your-host>:9909/api/portal/v1/jobs/getJobStatus
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
{
    "activeJobs": 2,
    "isEditable": true
}` %}}

Return a lightweight summary of the current job activity on the instance. Useful for quickly checking whether the system is busy without fetching the full job list.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token.

<b>Response Schema</b>

- `activeJobs`: The number of jobs in the `pending` or `running` state.
- `isEditable`: `true` if the caller is permitted to create maintenance jobs through [Create Job](/oem/portal-api-reference/jobs/create/), otherwise `false`.

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.

{{% /apiEndpointCard %}}
