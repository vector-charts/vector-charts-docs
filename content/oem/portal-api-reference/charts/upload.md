---
title: "Upload File"
weight: 1
menu:
  oem:
    parent: "portal_api_reference_charts"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/portal/v1/charts/upload" title="Upload Chart" request=`POST https://<your-host>:9909/api/portal/v1/charts/upload
Authorization: Bearer <token>
Content-Type: multipart/form-data

file: [binary file data]` response=`Status Code: 200 OK
Response Body:
{
    "upload": {
        "id": 5,
        "filename": "US5MA10M.000",
        "fileSize": 104857600,
        "status": "pending"
    }
}` %}}

Upload an S-57 or S-63 exchange set, chart file, or permit to the OEM instance.

When a file is uploaded, an upload record is created with status `pending`, and a background job is kicked off to ingest the data. Use [List Uploads](/oem/portal-api-reference/charts/list-uploads/) to monitor progress.

If any uploaded cells match existing cells on the account, the existing data is overwritten. Uploading a new permit file replaces the existing permit.

<b>Authentication</b>

This endpoint requires a Bearer token in the `Authorization` header.

- **Authorization**: `Bearer <token>`. A valid Portal API session token or API token.

<b>Request Body</b>

The request body should be `multipart/form-data` encoded.

- **file**: The chart file to upload. See [Charts](/oem/portal-api-reference/charts/) for the list of accepted formats and the maximum upload size.

<b>Response Schema</b>

On success, the endpoint returns the newly created upload record.

- `upload.id`: The unique identifier for the upload. Use this with [Get Upload](/oem/portal-api-reference/charts/get-upload/) and [Delete Upload](/oem/portal-api-reference/charts/delete-upload/).
- `upload.filename`: The sanitized original filename.
- `upload.fileSize`: The size of the uploaded file in bytes.
- `upload.status`: The initial status of the upload. Always `pending` on a successful response.

<b>Error Responses</b>

- **400 Bad Request**: No file was provided, the file type is not accepted, or the file exceeds the maximum size.
- **401 Unauthorized**: The `Authorization` header is missing or the token is not valid.

{{% /apiEndpointCard %}}
