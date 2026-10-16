---
title: "Unified DEM"
weight: 7
menu:
  main:
    parent: "elevation_api"
    weight: 7
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---



{{% apiEndpointCard method="GET" path="/api/v2/tiles/elevation-unified-v1/{z}/{x}/{y}.png?token=<token string>" title="Unified DEM" request=`GET https://api.vectorcharts.com/api/v2/tiles/elevation-unified-v1/12/1205/1539.png?token=299ce9bf4f244300a96f3926240f9c0d` response=`Status Code: 200 OK
Content-Type: image/png

... binary PNG image ...` %}}

Returns a 256×256 Terrain-RGB elevation tile that combines basemap elevation with high-resolution nautical chart bathymetry (for example uploaded or licensed S-102 grids).

Unlike [S-102 Bathymetry DEM]({{< relref "s102-bathymetry-dem.md" >}}) and [S-102 Bathymetry Gradient]({{< relref "s102-bathymetry-gradient.md" >}}), this tile includes basemap terrain and covers **land and sea**. Elevations are relative to mean sea level (MSL) and encoded with Mapbox Terrain-RGB (`encoding: mapbox`).

The same tile is also available as WebP:

`GET /api/v2/tiles/elevation-unified-v1/{z}/{x}/{y}.webp`

Use this endpoint as a `raster-dem` source for hillshade or 3D terrain across the full map extent.

<b>Path Parameters</b>

- **z** <span style="color:red;">(Required)</span>: Zoom level of the tile.
- **x** <span style="color:red;">(Required)</span>: X coordinate of the tile.
- **y** <span style="color:red;">(Required)</span>: Y coordinate of the tile.

<b>Query Parameters</b>

- **token** <span style="color:red;">(Required)</span>: Vector Charts API token. (Alternatively, send `Authorization: Bearer <token>`.)

<b>Example Usage</b><br/><br/>
As a Mapbox GL JS terrain source:

<pre class="light">
map.addSource('unified-dem', {
    type: 'raster-dem',
    tiles: [
        'https://api.vectorcharts.com/api/v2/tiles/elevation-unified-v1/{z}/{x}/{y}.png?token=&lt;token&gt;'
    ],
    tileSize: 256,
    maxzoom: 22,
    encoding: 'mapbox'
});

map.setTerrain({ source: 'unified-dem', exaggeration: 1.5 });
</pre>

Decode height from a pixel with:

<pre class="light">
height = -10000 + ((R * 65536 + G * 256 + B) * 0.1)
</pre>

{{% /apiEndpointCard %}}
