---
title: "Upload Charts"
weight: 1
menu:
  main:
    parent: "chart_api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/v1/charts/upload" title="Upload Charts" request=`POST https://api.vectorcharts.com/api/v1/charts/upload
Authorization: Bearer <token>
Content-Type: multipart/form-data

file: [binary file data]` response=`Status Code: 200 OK
Response Body:
{
    "upload": {
        "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
        "filename": "US5MA10M.000",
        "fileSize": 104857600,
        "status": "pending"
    }
}` %}}

<span style="color:#9e6c2e">Feature Preview: some features of this endpoint are limited to enterprise or self-hosted customers.</span>

Upload custom S-57 charts, S-63 charts, or S-63 permits to your Vector Charts account. The file is streamed directly to storage, and the response is returned once the upload is complete. A background job is then created to index the chart data — the `status` field in the response will be `"pending"` until processing finishes.

If any uploaded cells match existing cells on the account, the existing data will be overwritten. Similarly, uploading a new permit file will replace the existing permit.

The following input formats are accepted:

- **S-57 Exchange Set** (`.zip`): A zipped S-57 exchange set containing one or more ENC cells.
- **S-63 Exchange Set** (`.zip`): A zipped S-63 encrypted exchange set, along with the corresponding `.prm` permit file.
- **S-57 File** (`.000`): A standalone S-57 ENC cell file.
- **S-63 Permit File** (`.prm` or `PERMIT.TXT`): A standalone permit file for decrypting S-63 charts.

Maximum file size is 1 GB.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization** <span style="color:red;">(Required)</span>: `Bearer <token>` — a valid Vector Charts API token.

<b>Request Body</b>

*The request body should be `multipart/form-data` encoded.*

- **file** <span style="color:red;">(Required)</span>: The chart file to upload. Accepted formats: `.zip` (S-57 or S-63 exchange set), `.000` (single S-57 cell), or `.prm` (S-63 permit file). Maximum 1 GB.

<b>Response Schema</b>

On success, the endpoint returns the created upload record:

- `id`: Unique identifier for the upload.
- `filename`: The sanitized original filename.
- `fileSize`: Size of the uploaded file in bytes.
- `status`: Initial status of the upload, `"pending"`. The file will be processed asynchronously by a background job.

<b>Error Responses</b>

- **400 Bad Request**: Invalid file type or no file provided (e.g. `File type .pdf not allowed. Allowed types: .000, .zip, .txt, .prm`).
- **400 Bad Request**: File exceeds the 1 GB size limit.

{{% /apiEndpointCard %}}