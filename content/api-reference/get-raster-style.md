---
title: "Get Raster Style"
weight: 4
menu:
  main:
    parent: "api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/v1/styles/raster.json?token=<token string>" title="Get Raster Style" request=`GET https://api.vectorcharts.com/api/v1/styles/raster.json?token=299ce9bf4f244300a96f3926240f9c0d` response=`{
  "version": 8,
  "sources": {
    "raster-tiles": {
      "type": "raster",
      "tiles": [
        "https://api.vectorcharts.com/api/v2/tiles/enc-raster-v2/{z}/{x}/{y}.png?token=..."
      ],
      "tileSize": 256,
      "attribution": "© VectorCharts.com"
    }
  },
  "layers": [
    {
      "id": "raster-tiles",
      "type": "raster",
      "source": "raster-tiles",
      "minzoom": 0,
      "maxzoom": 18
    }
  ]
}` %}}

<span style="color:#9e6c2e">Business Plan Only: The referenced raster tiles are restricted to business-tier customers.</span>

Returns a minimal Mapbox-compatible style document that references the [raster tile endpoint](/api-reference/get-png/). Use this URL as the style for renderers that consume Mapbox-style raster sources.

Style query parameters are forwarded onto the underlying tile URLs so the same theming options used by the [vector style API](/api-reference/get-mvt/) apply when the tiles are fetched.

<b>Query Parameters</b>

- **token** <span style="color:red;">(Required)</span>: Vector Charts API token.

See [Get Vector Style](/api-reference/get-mvt/) for the full list of supported style query parameters.

<b>Response</b>

On success, returns a Mapbox Style Specification JSON document with a single raster source pointing at `/api/v2/tiles/enc-raster-v2/{z}/{x}/{y}.png`.

<b>Example Usage</b><br/><br/>
in Leaflet with maplibre-gl-leaflet:

<pre class="light">
L.maplibreGL({
  style: "https://api.vectorcharts.com/api/v1/styles/raster.json?token=&lt;token&gt;"
}).addTo(map);
</pre>

{{% /apiEndpointCard %}}
