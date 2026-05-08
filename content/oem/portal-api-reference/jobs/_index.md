---
title: "Jobs"
weight: 6
menu:
  oem:
    parent: "portal_api_reference"
    identifier: "portal_api_reference_jobs"
---

The Jobs endpoints expose the background work running inside an OEM instance. Jobs are used for chart ingestion, scheduled maintenance, and other long-running operations. The Portal API allows you to inspect jobs that are already in flight, and to start a small set of maintenance jobs on demand.

## Job Types

The following job types can be started through [Create Job](/oem/portal-api-reference/jobs/create/):

- `refresh-public-charts`: Re-download the latest public ENC chart catalog from NOAA and ingest any new or updated cells.
- `clear-tiles`: Clear the on-disk tile cache. Subsequent tile requests will be re-rendered from the underlying chart data.
- `vacuum-analyze`: Run `VACUUM ANALYZE` on the chart database. Useful after large ingestions or deletions.

Other job types may appear in [List Jobs](/oem/portal-api-reference/jobs/list/) responses (for example, `user-upload` jobs created by the chart upload flow), but cannot be started directly.

## Job States

A job progresses through the following states:

- `pending`: The job has been created and is waiting for a worker.
- `running`: A worker is actively executing the job.
- `completed`: The job finished successfully.
- `failed`: The job encountered an error.
- `cancelled`: The job was cancelled before it finished.
