---
title: "Get Reports (MVT)"
weight: 6
---

{{% apiEndpointCard method="GET" path="/api/v1/user-reports/tiles/{z}/{x}/{y}.mvt" title="Get Reports (MVT)" request=`GET https://api.vectorcharts.com/api/v1/user-reports/tiles/12/1240/1515.mvt?token=<token>&includeBathymetry=true` response=`Status Code: 200 OK
Content-Type: application/vnd.mapbox-vector-tile
(binary Mapbox Vector Tile)` %}}

Returns active (non-deleted, non-expired) user reports intersecting the given map tile as a Mapbox vector tile (MVT).

This is the tile URL used by the `userReports` source when `showUserReports=true` is set on the style. Feature properties include report type, vote counts, label, optional description, and `is_owner` for the calling token.

<b>Authentication</b>

Requires a Bearer token in the `Authorization` header or a `token` query parameter.

<b>Path Parameters</b>

- **z**: Tile zoom level.
- **x**: Tile column.
- **y**: Tile row.

<b>Query Parameters</b>

- **includeBathymetry** (Optional): If `true`, also include bathymetry track line features in the tile. Defaults to `false`.

<b>Layers</b>

- **user_reports**: Point features for user reports.
- **user_reported_bathymetry** (when `includeBathymetry=true`): LineString segments with a per-segment `depth` value and track properties: `platform_name`, `start_time`, `end_time`, `created_at`, `point_count`, `min_depth`, `max_depth`, `length_m`.

Tiles omit report and bathymetry data below the style min zoom (`z < 11`).

<b>Error Responses</b>

- **400 Bad Request**: Invalid tile coordinates.
- **401 Unauthorized**: Token is missing or invalid.

{{% /apiEndpointCard %}}
