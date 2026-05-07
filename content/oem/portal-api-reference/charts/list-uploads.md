---
title: "List Uploads"
weight: 3
menu:
  oem:
    parent: "portal_api_reference_charts"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/portal/v1/charts/uploads" title="List Uploads" request=`GET https://<your-host>:9909/api/portal/v1/charts/uploads?limit=10&offset=0
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
{
    "uploads": [
        {
            "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
            "filename": "US5MA10M.000",
            "fileSize": 104857600,
            "status": "completed",
            "createdAt": 1736942400000,
            "updatedAt": 1736946000000,
            "uploaderEmail": "example@zydromarine.com",
            "totalCharts": 12,
            "expiredCharts": 2,
            "logs": [
                {
                    "timestamp": 1736942410000,
                    "type": "info",
                    "message": "Indexing 12 cells"
                }
            ]
        }
    ],
    "pagination": {
        "limit": 10,
        "offset": 0
    }
}` %}}

List the chart uploads on the account, ordered most recent first. Each upload record includes its current processing status and aggregated logs from the ingestion job, which is suitable for polling progress after a call to [Upload Chart](/oem/portal-api-reference/charts/upload/).

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token.

<b>Query Parameters</b>

- **limit** (Optional): Maximum number of uploads to return. Defaults to `100`.
- **offset** (Optional): Number of uploads to skip from the start of the list. Defaults to `0`. Combine with `limit` to page through results.

<b>Response Schema</b>

The endpoint returns a paginated list of upload records.

- `uploads`: An array of upload records.
- `uploads[].id`: The unique identifier for the upload.
- `uploads[].filename`: The sanitized original filename.
- `uploads[].fileSize`: The size of the uploaded file in bytes.
- `uploads[].status`: The processing status of the upload. See [Charts](/oem/portal-api-reference/charts/) for the full lifecycle.
- `uploads[].createdAt`: Timestamp when the upload was received, in milliseconds since unix epoch.
- `uploads[].updatedAt`: Timestamp when the upload record was last modified, in milliseconds since unix epoch.
- `uploads[].uploaderEmail`: The email of the user who uploaded the file.
- `uploads[].totalCharts`: The total number of chart cells contained in the upload.
- `uploads[].expiredCharts`: The number of chart cells in the upload that are past their expiry date.
- `uploads[].logs`: An array of log entries emitted by the ingestion job. Each entry has `timestamp` (milliseconds since unix epoch), `type` (one of `info`, `warning`, `error`), and `message`.
- `pagination.limit`: The `limit` value applied to the request.
- `pagination.offset`: The `offset` value applied to the request.

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.

{{% /apiEndpointCard %}}
