---
title: "Get Vector Tile"
weight: 3
menu:
  oem:
    parent: "api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/v2/tiles/enc-v2/{z}/{x}/{y}.mvt" title="Get Vector Tile" request=`GET https://<your-host>:9909/api/v2/tiles/enc-v2/12/1240/1515.mvt
Authorization: Bearer <token>` response=`Status Code: 200 OK
Content-Type: application/x-protobuf

... binary MVT protobuf ...` %}}

Returns a Mapbox Vector Tile containing rendered chart data for the given XYZ tile coordinates. Each tile combines basemap geometry, ENC features from all overlapping cells, and runtime layers into a single protobuf payload.

Renderers do not usually call this endpoint directly. Instead, point Mapbox or another vector-capable renderer at the [vector style endpoint](/oem/api-reference/get-style/), which references this URL internally.

<b>Authentication</b>

This endpoint accepts a Bearer token in the `Authorization` header or a `token` query parameter. See [Authentication](/oem/api-reference/) for details.

<b>Path Parameters</b>

- **z**: Zoom level. Must be between `0` and `16` inclusive.
- **x**: Tile column.
- **y**: Tile row.

<b>Response</b>

On success, returns a binary MVT protobuf with `Content-Type: application/x-protobuf`. The tile is empty (no layers) outside of charted areas.

<b>Error Responses</b>

- **400 Bad Request**: The `z`, `x`, or `y` parameter is out of range, or `z` is greater than `16`.
- **401 Unauthorized**: The token is missing or not valid.

{{% /apiEndpointCard %}}
