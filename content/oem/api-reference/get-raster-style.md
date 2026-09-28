---
title: "Get Raster Style"
weight: 4
menu:
  oem:
    parent: "api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/v1/styles/raster.json" title="Get Raster Style" request=`GET https://<your-host>:9909/api/v1/styles/raster.json
Authorization: Bearer <token>` response=`{
  "version": 8,
  "sources": {
    "raster-tiles": {
      "type": "raster",
      "tiles": [
        "https://<your-host>:9909/api/v2/tiles/enc-raster-v2/{z}/{x}/{y}.png?token=..."
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

Returns a minimal Mapbox-compatible style document that references the [raster tile endpoint](/oem/api-reference/get-png/). Use this URL as the style for renderers that consume Mapbox-style raster sources.

Style query parameters are forwarded onto the underlying tile URLs so the same theming options used by the [vector style API](/oem/api-reference/get-style/) apply when the tiles are fetched.

<b>Authentication</b>

This endpoint accepts a Bearer token in the `Authorization` header or a `token` query parameter. See [Authentication](/oem/api-reference/) for details.

<b>Query Parameters</b>

- **token** (Optional): API token. Prefer the `Authorization` header when possible; use this when the client cannot set custom headers.

See [Get Vector Style](/oem/api-reference/get-style/) for the full list of supported style query parameters.

<b>Response</b>

On success, returns a Mapbox Style Specification JSON document with a single raster source pointing at `/api/v2/tiles/enc-raster-v2/{z}/{x}/{y}.png`.

<b>Example Usage</b><br/><br/>
in Leaflet with maplibre-gl-leaflet:

<pre class="light">
L.maplibreGL({
  style: "https://&lt;your-host&gt;:9909/api/v1/styles/raster.json?token=&lt;token&gt;"
}).addTo(map);
</pre>

{{% /apiEndpointCard %}}
