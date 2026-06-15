---
title: "Get User Reports MVT Tile"
weight: 5
menu:
  crowdsourced:
    parent: "user_report_api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/v1/user-reports/tiles/{z}/{x}/{y}.mvt" title="Get User Reports MVT Tile" request=`GET https://api.vectorcharts.com/api/v1/user-reports/tiles/12/1240/1515.mvt?token=<token>` response=`Status Code: 200 OK
Content-Type: application/vnd.mapbox-vector-tile
(binary Mapbox Vector Tile)` %}}

Returns active (non-deleted, non-expired) user reports intersecting the given slippy-map tile as a Mapbox vector tile (MVT).

The `user_reports` source layer includes point features with report attributes: `id`, `report_type`, `properties` (JSON string), `valid_vote_count`, `invalid_vote_count`, `external_user_id`, `namespace`, `created_at`, and `updated_at`.

<b>Map style integration</b>

The vector chart style (`/api/v1/styles/base.json`) includes a `userReports` vector source pointing at this endpoint and a symbol layer that renders each report with the `DANGER01` alert icon. Query feature properties in the client to show report details on click.

<b>Authentication</b>

Requires a Bearer token in the `Authorization` header or a `token` query parameter.

<b>Path Parameters</b>

- **z**: Tile zoom level.
- **x**: Tile column.
- **y**: Tile row.

<b>Error Responses</b>

- **400 Bad Request**: Invalid tile coordinates.
- **401 Unauthorized**: Token is missing or invalid.

{{% /apiEndpointCard %}}
