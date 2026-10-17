---
title: "S-102 Bathymetry Gradient"
weight: 5
menu:
  main:
    parent: "elevation_api"
    weight: 5
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---



{{% apiEndpointCard method="GET" path="/api/v2/tiles/raster-depth-gradient-v1/{z}/{x}/{y}.png?token=<token string>" title="S-102 Bathymetry Gradient" request=`GET https://api.vectorcharts.com/api/v2/tiles/raster-depth-gradient-v1/14/4824/6160.png?token=299ce9bf4f244300a96f3926240f9c0d` response=`Status Code: 200 OK
Content-Type: image/png

... binary PNG image ...` %}}

Returns a 256×256 PNG tile of high-resolution bathymetry depth from S-102 grids. Pixels with no depth data (or land) are transparent.

By default the tile encodes depth in the red channel for client-side colorization (Mapbox GL JS ≥ 3 `raster-color` / `raster-value`). Set `portrayal=rgba` to receive a pre-colorized S-52 depth band image instead (used by MapLibre-compatible style rendering).

You can also enable this layer through the [Get Vector Style](/api-reference/get-mvt/) endpoint with `showRasterBathymetry=true`.

Depth data is available from zoom **10** and above. Below that zoom, the tile is fully transparent.

<b>Path Parameters</b>

- **z** <span style="color:red;">(Required)</span>: Zoom level of the tile.
- **x** <span style="color:red;">(Required)</span>: X coordinate of the tile.
- **y** <span style="color:red;">(Required)</span>: Y coordinate of the tile.

<b>Query Parameters</b>

- **token** <span style="color:red;">(Required)</span>: Vector Charts API token. (Alternatively, send `Authorization: Bearer <token>`.)
- **portrayal** (Optional): Set to `rgba` for a server-colorized S-52 depth image. When omitted, depth is encoded in the red channel for client-side colorization.
- **theme** (Optional): Color scheme when `portrayal=rgba`. One of `day`, `dusk`, or `night`. Defaults to `day`.
- **depthLimit** (Optional): Safety contour in meters when `portrayal=rgba`. Controls S-52 shallow / safety / deep depth bands. Defaults to `3`.
- **renderSoloDatasetId** (Optional): When set, render only a single S-102 dataset (must be owned or accessible by the account for the API token).

<b>Example Usage</b><br/><br/>
As a Mapbox GL JS raster source with client-side colorization:

<pre class="light">
map.addSource('s102-depth', {
    type: 'raster',
    tiles: [
        'https://api.vectorcharts.com/api/v2/tiles/raster-depth-gradient-v1/{z}/{x}/{y}.png?token=&lt;token&gt;'
    ],
    tileSize: 256,
    minzoom: 10,
    maxzoom: 22
});
</pre>

{{% /apiEndpointCard %}}
