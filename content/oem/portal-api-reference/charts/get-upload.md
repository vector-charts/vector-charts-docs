---
title: "Get Upload"
weight: 4
menu:
  oem:
    parent: "portal_api_reference_charts"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/portal/v1/charts/uploads/{id}" title="Get Upload" request=`GET https://<your-host>:9909/api/portal/v1/charts/uploads/a1b2c3d4-e5f6-7890-abcd-ef1234567890
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
{
    "upload": {
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
}` %}}

Return the upload record with the given `id`. The upload must belong to the caller's account.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token.

<b>Path Parameters</b>

- **id**: The `id` of the upload to retrieve.

<b>Response Schema</b>

The endpoint returns a single upload record.

- `upload.id`: The unique identifier for the upload.
- `upload.filename`: The sanitized original filename.
- `upload.fileSize`: The size of the uploaded file in bytes.
- `upload.status`: The processing status of the upload. See [Charts](/oem/portal-api-reference/charts/) for the full lifecycle.
- `upload.createdAt`: Timestamp when the upload was received, in milliseconds since unix epoch.
- `upload.updatedAt`: Timestamp when the upload record was last modified, in milliseconds since unix epoch.
- `upload.uploaderEmail`: The email of the user who uploaded the file.
- `upload.totalCharts`: The total number of chart cells contained in the upload.
- `upload.expiredCharts`: The number of chart cells in the upload that are past their expiry date.
- `upload.logs`: An array of log entries emitted by the ingestion job. Each entry has `timestamp` (milliseconds since unix epoch), `type` (one of `info`, `warning`, `error`), and `message`.

<b>Error Responses</b>

- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.
- **404 Not Found**: No upload exists with the given `id` on the caller's account.

{{% /apiEndpointCard %}}
