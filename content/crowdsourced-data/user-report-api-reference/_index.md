---
title: "Overview"
weight: 1
menu:
  crowdsourced:
    title: "Overview"
    parent: "user_report_api_reference"
    weight: 1
---

Crowdsourced user reports are location-based observations submitted by users — for example hazards, accidents, weather, and wildlife sightings. Each report has a `reportType`, a latitude/longitude position, optional `properties` (such as a free-text `description`), vote counts, and an `isOwner` flag for the calling token.

Reports are scoped to a server-configured **namespace** (default `public`). Reports expire automatically after a configured age (default 24 hours). Soft-deleted reports remain in storage with `deletedAt` set and are excluded from tiles and default list responses.

These endpoints are available on both [Vector Charts Cloud](https://api.vectorcharts.com) and Vector Charts OEM. Replace the host in examples with your deployment's base URL.

## Report Types

Supported values: `hazard`, `accident`, `weather`, and `wildlife`. Legacy aliases such as `obstacle`, `uncharted_hazard`, and `fish` are accepted and normalized for display.

## Report Object

REST endpoints return a report object with these fields:

- **id**: UUID version 4
- **reportType**: Report category
- **latitude** / **longitude**: WGS84 decimal degrees
- **properties**: Arbitrary JSON metadata (use `description` for free-text notes)
- **upvoteCount** / **downvoteCount**: Aggregated vote totals
- **isOwner**: `true` when the authenticated API token user created this report
- **externalUserId**: Optional opaque client user identifier
- **createdAt** / **updatedAt**: Milliseconds since Unix epoch
- **expiredAt** / **deletedAt**: Null when active; set when expired or soft-deleted
- **namespace**: Namespace this report belongs to (matches server config)

## Displaying reports on the map

Enable the built-in user-report layers by adding `showUserReports=true` to the [Get Vector Style](/api-reference/get-mvt/) request:

<pre class="light">
const map = new mapboxgl.Map({
    style: "https://api.vectorcharts.com/api/v1/styles/base.json?token=&lt;token&gt;&showUserReports=true"
});
</pre>

When enabled, the style includes a `userReports` vector source pointing at `/api/v1/user-reports/tiles/{z}/{x}/{y}.mvt` and marker layers for each report.

## Querying reports directly

If you prefer not to use the built-in style layers — or need reports outside a map viewport — query the REST and tile endpoints directly:

- **[List Reports](/crowdsourced-data/user-report-api-reference/list/)** — paginated JSON feed of all active reports (optionally including deleted or expired)
- **[Get Reports (MVT)](/crowdsourced-data/user-report-api-reference/tile-mvt/)** — Mapbox vector tiles for custom style sources
- **[Get Reports (GeoJSON)](/crowdsourced-data/user-report-api-reference/tile-geojson/)** — GeoJSON FeatureCollections per slippy-map tile

Deleted and expired reports are omitted from tile responses. List responses exclude them by default unless `includeDeleted` / `includeExpired` are set.

## Authentication

All user report endpoints require a valid API token, either as:

- `Authorization: Bearer <token>`, or
- `?token=<token>` query parameter (useful for map tile and style URLs)

Create and vote require a token associated with a user identity. Delete is allowed for the report owner or an admin.

## Endpoints

| Method | Path | Description |
| --- | --- | --- |
| `POST` | `/api/v1/user-reports` | Create a report |
| `POST` | `/api/v1/user-reports/{id}/votes` | Vote on a report |
| `DELETE` | `/api/v1/user-reports/{id}` | Soft-delete a report |
| `GET` | `/api/v1/user-reports` | List reports |
| `GET` | `/api/v1/user-reports/tiles/{z}/{x}/{y}.mvt` | Vector tile |
| `GET` | `/api/v1/user-reports/tiles/{z}/{x}/{y}.json` | GeoJSON tile |
