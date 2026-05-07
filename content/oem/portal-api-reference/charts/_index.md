---
title: "Charts"
weight: 4
menu:
  oem:
    parent: "portal_api_reference"
    identifier: "portal_api_reference_charts"
---

The Charts endpoints manage the nautical chart data on a Vector Charts OEM deployment. Customers can upload S-57 and S-63 chart cells, monitor processing of those uploads, and retrieve the S-63 user permit assigned to their account.

## Chart Formats

The following file formats are accepted by the upload endpoint:

- **S-57 Exchange Set** (`.zip`): A zipped S-57 exchange set containing one or more ENC cells.
- **S-63 Exchange Set** (`.zip`): A zipped S-63 encrypted exchange set, along with the corresponding `.prm` permit file.
- **S-57 File** (`.000`): A standalone S-57 ENC cell file.
- **S-63 Permit File** (`.prm` or `PERMIT.TXT`): A standalone permit file for decrypting S-63 charts.

Maximum upload size is 1 GB.

## Upload Lifecycle

Chart uploads are processed asynchronously. When a file is uploaded, an upload record is created with status `pending`, and a background job is started to ingest the chart data. The status of an upload progresses through the following values:

- `pending`: The file has been received and is queued for processing.
- `processing`: A processing job is actively working on the upload.
- `completed`: Processing finished successfully and the charts are available for use.
- `failed`: Processing encountered an error. See the upload's `logs` field for details.
- `cancelled`: Processing was cancelled, either by deletion of the upload or by an administrator.

Use [List Uploads](/oem/portal-api-reference/charts/list-uploads/) to poll for status changes after an upload.
