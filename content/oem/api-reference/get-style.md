---
title: "Get Vector Style"
weight: 2
menu:
  oem:
    parent: "api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/v1/styles/base.json" title="Get Vector Style" request=`GET https://<your-host>:9909/api/v1/styles/base.json?theme=day&depthLimit=10
Authorization: Bearer <token>` response=`... style json document ...` %}}

Returns a Mapbox-compatible style document for rendering vector charts. The style references the `enc-v2` vector tile endpoint and bakes in the colors, fonts, and display toggles selected via query parameters.

This is the URL to pass to a vector-capable map renderer as its base style.

<b>Authentication</b>

This endpoint accepts a Bearer token in the `Authorization` header or a `token` query parameter. See [Authentication](/oem/api-reference/) for details.

<b>Query Parameters</b>

- **styleId** (Optional): Identifier of a custom style created via the [Portal API](/oem/portal-api-reference/styles/). When set, the style's saved colors and settings override the defaults.
- **theme** (Optional): Color palette. One of `day`, `dusk`, or `night`. Defaults to `day`.
- **depthLimit** (Optional): Safety contour value. Areas shallower than this are shaded distinctly. Defaults to `3`.
- **depthUnits** (Optional): Units for depth soundings. One of `meters`, `feet`, or `fathoms`. Defaults to `meters`.
- **roundOffSoundings** (Optional): Round soundings to the nearest whole number. Defaults to `false`.
- **showLightSectors** (Optional): Draw light sector arcs around lighthouses. Defaults to `true`.
- **showEncBoundaries** (Optional): Outline the S-57 ENC chart cells. Defaults to `false`.
- **showPlaceNames** (Optional): Show names of landmarks and built-up areas. Defaults to `true`.
- **showOverscale** (Optional): Show an indication when the map is zoomed in beyond the source data's resolution. Defaults to `true`.
- **showNoData** (Optional): Show an indication where there is no ENC data. Defaults to `true`.
- **showSatellite** (Optional): Render a satellite imagery basemap underneath the chart. Defaults to `false`.
- **maskLandAreas** (Optional): When `showSatellite` is enabled, mask land areas with a flat fill so the chart symbology stays legible. Defaults to `false`.
- **hideLayers** (Optional): Comma-separated list of style layer IDs to hide.
- **showLayers** (Optional): Comma-separated list of style layer IDs to show. When set, all other layers are hidden.
- **glyphs** (Optional): Override the glyphs (fonts) URL used by the style. Must be URL-encoded.
- **font** (Optional): Override the font used for soundings and other text labels.

<b>Example Usage</b><br/><br/>
in Mapbox GL JS:

<pre class="light">
const map = new mapboxgl.Map({
    ...
    style: "https://&lt;your-host&gt;:9909/api/v1/styles/base.json?token=&lt;token&gt;&theme=day&depthLimit=10"
});
</pre>

{{% /apiEndpointCard %}}
