---
title: "Core API Overview"
weight: 1
menu:
  oem:
    title: "Overview"
    parent: "api_reference"
    weight: 1
---

The Core API serves chart tiles, ENC feature queries, and dataset attributions. It is the runtime surface that client applications call when rendering or querying charts.

The Core API is mounted at the root of the OEM server. For an OEM instance running at `https://<your-host>:9909`, the Core API base URL is:

<pre>
https://&lt;your-host&gt;:9909
</pre>

## Authentication

Core API requests are authenticated with an API token. Tokens are created and managed through the [Portal API](/oem/portal-api-reference/api-tokens/).

### Header Authentication

For server-side requests, send the token in an `Authorization` header:

<pre>
Authorization: Bearer &lt;token string&gt;
</pre>

### Query Parameter Authentication

Mapping libraries usually do not allow setting custom request headers when fetching tiles or styles. In that case, pass the token as a `token` query parameter instead:

<pre>
https://&lt;your-host&gt;:9909/api/v2/tiles/enc-v2/{z}/{x}/{y}.mvt?token=&lt;token string&gt;
</pre>

For example, in Mapbox GL JS:

<pre>
const map = new mapboxgl.Map({
    ...
    style: "https://&lt;your-host&gt;:9909/api/v1/styles/base.json?token=&lt;token string&gt;"
});
</pre>
