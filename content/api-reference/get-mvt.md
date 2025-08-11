---
title: "Get Vector Style"
weight: 2
menu:
  main:
    parent: "api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/v1/styles/base.json?token=<token string>" title="Get Vector Style" request=`GET https://api.vectorcharts.com/api/v1/styles/base.json?token=a8652e5b659c41ed86c0b6717d8b0b3f&theme=day&depthLimit=10` response=`... style json document ...` %}}
Returns the vector style JSON for use in Mapbox and other map renderers which support vector rendering.

This URL should be used as the base style.

<b>Query Parameters</b>

- **token** <span style="color:red;">(Required)</span>: Vector Charts API token.
- **styleId**: Identifier for a custom style.
- **theme**: Set to `day`, `dusk` or `night` to change color schemes.
- **depthLimit**: Sets the safety contour value in meters.
- **depthUnits**: Sets the units for depth soundings: `meters`, `feet`, or `fathoms` are valid.
- **showEncBoundaries**: Show an outline of the S-57 ENC chart cells. Defaults to `false`.
- **showPlaceNames**: Show names of landmarks & built-up areas. Defaults to `true`.
- **showOverscale**: Show an indication when the map is zoomed in too far. Defaults to `true`.
- **showNoData**: Show an indication where there is no ENC data. Defaults to `true`.
- **glyphs**: Override the glyphs (fonts) for the style with another URL. Must be a URL-encoded string.
- **font**: Override the font used for soundings and other textual elements.

<b>Example Usage</b><br/><br/>
in Mapbox GL JS:

<pre class="light">
const map = new mapboxgl.Map({
    ...
    style: "https://api.vectorcharts.com/api/v1/styles/base.json?token=&lt;token&gt;&theme=day&depthLimit=10"
});
</pre>

{{% /apiEndpointCard %}}