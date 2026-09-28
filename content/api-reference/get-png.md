---
title: "Get Tile (PNG)"
weight: 5
menu:
  main:
    parent: "api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/v2/tiles/enc-raster-v2/{z}/{x}/{y}.png?token=<token string>" title="Get Raster Tile" request=`GET https://api.vectorcharts.com/api/v2/tiles/enc-raster-v2/12/1240/1515.png?token=299ce9bf4f244300a96f3926240f9c0d` response=`Status Code: 200 OK
Content-Type: image/png

... binary PNG image ...` %}}

<span style="color:#9e6c2e">Business Plan Only: This endpoint is restricted to business-tier customers.</span>

Returns a 256×256 PNG raster tile of the chart at the given XYZ coordinates. The server renders the tile from the same ENC data used by the [vector style API](/api-reference/get-mvt/), then caches the result.

For renderers that consume Mapbox-style raster sources, use the [raster style endpoint](/api-reference/get-raster-style/) instead. That endpoint returns a minimal style document that references this tile URL.

<b>Path Parameters</b>

- **z** <span style="color:red;">(Required)</span>: Zoom level.
- **x** <span style="color:red;">(Required)</span>: Tile column.
- **y** <span style="color:red;">(Required)</span>: Tile row.

<b>Query Parameters</b>

- **token** <span style="color:red;">(Required)</span>: Vector Charts API token.
- **styleId**: Identifier for a custom style.
- **styleName**: Identifier for a custom style (finds the style by name).
- **theme**: Set to `day`, `dusk`, or `night` to change color schemes.
- **depthLimit**: Sets the safety contour value in meters.
- **depthUnits**: Units for depth soundings: `meters`, `feet`, or `fathoms`.

See [Get Vector Style](/api-reference/get-mvt/) for the full list of supported style query parameters.

<b>Response</b>

On success, returns a PNG image with `Content-Type: image/png`.

<b>Error Responses</b>

- **401 Unauthorized**: The token is missing, not valid, or the account is not on a business plan.
- **404 Not Found**: The `z`, `x`, or `y` parameter is out of range for the given zoom level.

<b>Example Usage</b><br/><br/>
in Leaflet with maplibre-gl-leaflet:

<pre class="light">
L.maplibreGL({
  style: "https://api.vectorcharts.com/api/v1/styles/raster.json?token=&lt;token&gt;"
}).addTo(map);
</pre>

{{% /apiEndpointCard %}}
