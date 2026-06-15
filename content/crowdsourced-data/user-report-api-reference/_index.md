---
title: "User Report API Overview"
weight: 1
menu:
  crowdsourced:
    title: "Overview"
    parent: "user_report_api_reference"
    weight: 1
---

Crowdsourced user reports are spatially-defined suggestions about chart data submitted by users at a specific location. Each report has a fixed type, a latitude/longitude position, optional client metadata, and vote counts aggregated from other users.

Reports are scoped to a server-configured **namespace** (default `public`). Only reports in the configured namespace are visible via the API, included in streaming events, and replicated between peers. Peer instances must use the same namespace to exchange data.

Reports are global within a namespace: any authenticated user can list reports, fetch tile GeoJSON, vote, and receive streaming updates. Reports expire automatically after a server-configured TTL (default 24 hours) but remain stored in the database with an `isExpired` flag.

These endpoints are available on both [Vector Charts Cloud](https://api.vectorcharts.com) and Vector Charts OEM. Replace the host in examples with your deployment's base URL.

## Report Types

- `data_quality` — Data quality issue
- `hazard` — Navigation hazard
- `incident` — Incident
- `closure` — Closure or restriction
- `sos` — SOS / distress

## Report Object

REST endpoints return a report object with these fields:

- **id**: UUID version 4
- **reportType**: One of the report types above
- **position**: `{ latitude, longitude }` in WGS84 decimal degrees
- **properties**: Arbitrary JSON metadata
- **validVoteCount** / **invalidVoteCount**: Aggregated vote totals
- **externalUserId**: Optional opaque client user identifier
- **createdAt** / **updatedAt**: Milliseconds since Unix epoch
- **expiresAt**: Expiration timestamp
- **isExpired** / **isDeleted**: Lifecycle flags
- **namespace**: Namespace this report belongs to (matches server config)

## Authentication

All user report endpoints require a valid API token. See [Cloud authentication](/api-reference/api-authentication/) or the [OEM Core API overview](/oem/api-reference/) for header and query-parameter auth.

For WebSocket streaming, see [Streaming Events](/crowdsourced-data/getting-started/streaming-events/).
