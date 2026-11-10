---
title: "Elevation DEM"
weight: 1
menu:
  main:
    parent: "elevation_api"
    weight: 1
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/v2/tiles/elevation-unified-v1/{z}/{x}/{y}.png" title="Elevation DEM" request=`GET https://api.vectorcharts.com/api/v2/tiles/elevation-unified-v1/12/1205/1539.png
Authorization: Bearer <token>` response=`Status Code: 200 OK
Content-Type: image/png

... binary PNG image ...` %}}

Returns a 256×256 elevation tile in [Mapbox Terrain-RGB](https://docs.mapbox.com/data/tilesets/reference/mapbox-terrain-rgb-v1/) encoding. Values are meters relative to mean sea level (MSL) and cover both land and sea, combining basemap terrain with chart bathymetry where available.

Also available as WebP: `GET /api/v2/tiles/elevation-unified-v1/{z}/{x}/{y}.webp`

Use as a Mapbox/MapLibre `raster-dem` source for hillshade or 3D terrain.

<b>Authentication</b>

This endpoint accepts a Bearer token in the `Authorization` header or a `token` query parameter. See [Authentication](/api-reference/api-authentication/) for details.

<b>Path Parameters</b>

- **z** <span style="color:red;">(Required)</span>: Zoom level of the tile.
- **x** <span style="color:red;">(Required)</span>: X coordinate of the tile.
- **y** <span style="color:red;">(Required)</span>: Y coordinate of the tile.

<b>Example Usage</b><br/><br/>

<pre class="light">
map.addSource('elevation-dem', {
    type: 'raster-dem',
    tiles: [
        'https://api.vectorcharts.com/api/v2/tiles/elevation-unified-v1/{z}/{x}/{y}.png?token=&lt;token&gt;'
    ],
    tileSize: 256,
    maxzoom: 22,
    encoding: 'mapbox'
});

map.setTerrain({ source: 'elevation-dem', exaggeration: 1.5 });
</pre>

Decode height from a pixel with:

<pre class="light">
height = -10000 + ((R * 65536 + G * 256 + B) * 0.1)
</pre>

{{% /apiEndpointCard %}}
