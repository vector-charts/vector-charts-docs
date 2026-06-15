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

Reports expire automatically after a server-configured age (default 24 hours). Expired reports have `expiredAt` set and remain in the database.

These endpoints are available on both [Vector Charts Cloud](https://api.vectorcharts.com) and Vector Charts OEM. Replace the host in examples with your deployment's base URL.

## Report Types

Common examples include `data_quality`, `hazard`, `incident`, `closure`, and `sos`. The server does not enforce a fixed list.

## Report Object

REST endpoints return a report object with these fields:

- **id**: UUID version 4
- **reportType**: Free-form string label for the report category
- **latitude** / **longitude**: WGS84 decimal degrees
- **properties**: Arbitrary JSON metadata
- **validVoteCount** / **invalidVoteCount**: Aggregated vote totals
- **externalUserId**: Optional opaque client user identifier
- **createdAt** / **updatedAt**: Milliseconds since Unix epoch
- **expiredAt** / **deletedAt**: Null when active; set when expired or soft-deleted
- **namespace**: Namespace this report belongs to (matches server config)

For Mapbox vector tiles (recommended for map styles), see [Get User Reports MVT Tile](/crowdsourced-data/user-report-api-reference/tile-mvt/).

## Authentication

All user report endpoints require a valid API token. See [Cloud authentication](/api-reference/api-authentication/) or the [OEM Core API overview](/oem/api-reference/) for header and query-parameter auth.

For WebSocket streaming, see [Streaming Events](/crowdsourced-data/getting-started/streaming-events/).
