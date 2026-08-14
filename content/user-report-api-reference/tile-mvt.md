---
title: "Get Reports (MVT)"
weight: 6
---

{{% apiEndpointCard method="GET" path="/api/v1/user-reports/tiles/{z}/{x}/{y}.mvt" title="Get Reports (MVT)" request=`GET https://api.vectorcharts.com/api/v1/user-reports/tiles/12/1240/1515.mvt?token=<token>` response=`Status Code: 200 OK
Content-Type: application/vnd.mapbox-vector-tile
(binary Mapbox Vector Tile)` %}}

Returns active (non-deleted, non-expired) user reports intersecting the given slippy-map tile as a Mapbox vector tile (MVT).

This is the tile URL used by the `userReports` source when `showUserReports=true` is set on the style. Feature properties include report type, vote counts, label, optional description, and `is_owner` for the calling token.

Tiles are cached privately per requesting token (`Cache-Control: private, max-age=60`) because ownership is viewer-specific.

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
