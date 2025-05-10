---
title: "Get Vector Style"
weight: 2
menu:
  main:
    parent: "api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/v1/styles/base.json?token=<token string>" title="Get Vector Style" request=`n/a` response=`n/a` %}}
Returns the vector style JSON for use in Mapbox and other map renderers which support vector rendering.

This URL should be used as the base style.

For example, in Mapbox GL JS:

<pre class="light">
const map = new mapboxgl.Map({
    ...
    style: "https://api.vectorcharts.com/api/v1/styles/base.json?token=&lt;token string&gt;"
});
</pre>

{{% /apiEndpointCard %}}