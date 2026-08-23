---
title: "Get Tile (MVT)"
weight: 3
menu:
  main:
    parent: "api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/v2/tiles/enc-v2/{z}/{x}/{y}.mvt?token=<token string>" title="Get Vector Tile" request=`GET https://api.vectorcharts.com/api/v2/tiles/enc-v2/12/1240/1515.mvt?token=299ce9bf4f244300a96f3926240f9c0d` response=`Status Code: 200 OK
Content-Type: application/x-protobuf

... binary MVT protobuf ...` %}}

Returns a Mapbox Vector Tile containing chart data for the given XYZ tile coordinates. Each tile combines basemap geometry, ENC features from all overlapping cells, and runtime layers into a single protobuf payload.

Renderers do not usually call this endpoint directly. Instead, point Mapbox or another vector-capable renderer at the [vector style endpoint](/api-reference/get-mvt/), which references this URL internally.

<b>Path Parameters</b>

- **z** <span style="color:red;">(Required)</span>: Zoom level. Must be between `0` and `16` inclusive.
- **x** <span style="color:red;">(Required)</span>: Tile column.
- **y** <span style="color:red;">(Required)</span>: Tile row.

<b>Query Parameters</b>

- **token** <span style="color:red;">(Required)</span>: Vector Charts API token.

<b>Response</b>

On success, returns a binary MVT protobuf with `Content-Type: application/x-protobuf`. The tile is empty (no layers) outside of charted areas.

<b>Error Responses</b>

- **400 Bad Request**: The `z`, `x`, or `y` parameter is out of range, or `z` is greater than `16`.
- **401 Unauthorized**: The token is missing or not valid.

{{% /apiEndpointCard %}}
