---
title: "Get Raster Tile"
weight: 4
menu:
  oem:
    parent: "api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/v2/tiles/raster-v1/{z}/{x}/{y}.png" title="Get Raster Tile" request=`GET https://<your-host>:9909/api/v2/tiles/raster-v1/12/1240/1515.png
Authorization: Bearer <token>` response=`Status Code: 200 OK
Content-Type: image/png

... binary PNG image ...` %}}

Returns a 256x256 PNG raster tile of the chart at the given XYZ coordinates. The server renders the tile by drawing the same vector data described in [Get Vector Tile](/oem/api-reference/get-mvt/) onto a bitmap with the default day-mode style, then caches the result.

For renderers that consume Mapbox-style raster sources, point them at `/api/v1/styles/raster.json?token=<token string>`. That endpoint returns a minimal style document referencing this tile URL.

<b>Authentication</b>

This endpoint accepts a Bearer token in the `Authorization` header or a `token` query parameter. See [Authentication](/oem/api-reference/) for details.

<b>Path Parameters</b>

- **z**: Zoom level. Must be between `0` and `22` inclusive.
- **x**: Tile column.
- **y**: Tile row.

<b>Response</b>

On success, returns a PNG image with `Content-Type: image/png`.

<b>Error Responses</b>

- **401 Unauthorized**: The token is missing or not valid.
- **404 Not Found**: The `z`, `x`, or `y` parameter is out of range for the given zoom level.

{{% /apiEndpointCard %}}
