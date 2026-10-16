---
title: "S-102 Bathymetry DEM"
weight: 6
menu:
  main:
    parent: "elevation_api"
    weight: 6
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---



{{% apiEndpointCard method="GET" path="/api/v2/tiles/raster-elevation-rgb-v1/{z}/{x}/{y}.png?token=<token string>" title="S-102 Bathymetry DEM" request=`GET https://api.vectorcharts.com/api/v2/tiles/raster-elevation-rgb-v1/14/4824/6160.png?token=299ce9bf4f244300a96f3926240f9c0d` response=`Status Code: 200 OK
Content-Type: image/png

... binary PNG image ...` %}}

Returns a 256×256 opaque PNG tile in [Mapbox Terrain-RGB](https://docs.mapbox.com/data/tilesets/reference/mapbox-terrain-rgb-v1/) encoding (`encoding: mapbox`), derived from S-102 bathymetry.

- Where S-102 depth is present (and not on land), elevation is `-depth` meters (seafloor relative to MSL).
- Pixels with no bathymetry, or on land, are encoded as elevation **0**.
- Below zoom **14**, every pixel is elevation 0.

Visibility, coverage, and shoreline land-masking match [S-102 Bathymetry Gradient]({{< relref "s102-bathymetry-gradient.md" >}}). Use this endpoint as a `raster-dem` source for client-side hillshade or 3D terrain over S-102 coverage.

For land + sea elevation that also includes basemap terrain outside S-102 coverage, see [Unified DEM]({{< relref "unified-dem.md" >}}).

<b>Path Parameters</b>

- **z** <span style="color:red;">(Required)</span>: Zoom level of the tile.
- **x** <span style="color:red;">(Required)</span>: X coordinate of the tile.
- **y** <span style="color:red;">(Required)</span>: Y coordinate of the tile.

<b>Query Parameters</b>

- **token** <span style="color:red;">(Required)</span>: Vector Charts API token. (Alternatively, send `Authorization: Bearer <token>`.)
- **renderSoloDatasetId** (Optional): When set, render only a single S-102 dataset (must be owned or accessible by the account for the API token).

<b>Example Usage</b><br/><br/>
As a Mapbox GL JS terrain / hillshade source:

<pre class="light">
map.addSource('s102-dem', {
    type: 'raster-dem',
    tiles: [
        'https://api.vectorcharts.com/api/v2/tiles/raster-elevation-rgb-v1/{z}/{x}/{y}.png?token=&lt;token&gt;'
    ],
    tileSize: 256,
    maxzoom: 22,
    encoding: 'mapbox'
});

map.addLayer({
    id: 's102-hillshade',
    type: 'hillshade',
    source: 's102-dem'
});

// Or enable 3D terrain:
// map.setTerrain({ source: 's102-dem', exaggeration: 1.5 });
</pre>

Decode height from a pixel with:

<pre class="light">
height = -10000 + ((R * 65536 + G * 256 + B) * 0.1)
</pre>

{{% /apiEndpointCard %}}
