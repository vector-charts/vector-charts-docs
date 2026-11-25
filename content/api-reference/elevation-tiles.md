---
title: "Get Elevation Tile"
weight: 5.7
menu:
  main:
    parent: "api_reference"
    name: "Elevation tiles"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/v2/tiles/elevation-unified-v1/{z}/{x}/{y}.png" title="Get Elevation Tile" request=`GET https://api.vectorcharts.com/api/v2/tiles/elevation-unified-v1/14/2620/6334.png?token=YOUR_API_TOKEN` response=`Status Code: 200 OK
Content-Type: image/png
X-Vector-Charts-Cache: miss

... 256×256 Mapbox Terrain-RGB image ...` %}}

Returns one XYZ tile of the default elevation surface (`clamp` `none`, mean sea level) as Mapbox Terrain-RGB. The same path with a `.webp` extension returns `Content-Type: image/webp`. Both images use the same packing. The tile is 256×256 pixels.

Decode a pixel to meters, positive upward:

<pre>
heightMeters = -10000 + ((red * 65536 + green * 256 + blue) * 0.1)
</pre>

That is the `mapbox` raster-DEM encoding. Negative meters are below mean sea level. See [Elevation](/api-reference/query-elevation/) for the terrain and S-102 sources, the sign convention, and zoom. The server accepts `z` from 0 through 22. Bathymetry detail exists at zoom 14, and higher zooms are overzooms of that tile.

<b>Authentication</b>

Pass the token as a query parameter so a map client can request the tile, or send `Authorization: Bearer YOUR_API_TOKEN`. See [Authentication](/api-reference/api-authentication/).

<b>Path Parameters</b>

- **z**: Zoom level, integer 0 through 22.
- **x**: Tile column, from 0 up to but not including `2^z`.
- **y**: Tile row, from 0 up to but not including `2^z`.

An index outside that grid, including a zoom above 22, is HTTP 400 with an empty body.

<b>Response</b>

On success the body is the image. `X-Vector-Charts-Cache` is `hit` or `miss`.

MapLibre GL JS, using the PNG tiles:

<pre>
map.addSource("elevation", {
  type: "raster-dem",
  tiles: [
    "https://api.vectorcharts.com/api/v2/tiles/elevation-unified-v1/{z}/{x}/{y}.png?token=YOUR_API_TOKEN"
  ],
  encoding: "mapbox",
  tileSize: 256,
  maxzoom: 14
});
</pre>

`maxzoom: 14` keeps the client from requesting overzoomed tiles. The server still renders zooms 15 through 22 if you ask for them.

<b>Error Responses</b>

- **400**: Tile index is outside the grid. The body is empty.
- **401** and **403**: Same authentication and Cloud billing results as [Elevation](/api-reference/query-elevation/).
- **502** / **503** / **500**: The elevation engine could not render the tile. Messages match the table on [Elevation](/api-reference/query-elevation/).

{{% /apiEndpointCard %}}
