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

### End Users

Some type of data regions available on the Vector Charts platform require reporting on the number of end-users accessing the data. 

To attribute a request to a specific end user of your application, pass an additional end-user identifier as either:

- Query parameter: `endUserId=<your-user-id>`
- Header: `X-Vector-Charts-End-User: <your-user-id>`

If both are present, the header is used. The value should be a stable identifier for one person in your system (at most 256 characters).

Reporting end users allows your Vector Charts OEM server to segment usage, and is required for some add-on data licenses that meter by end-user count.

For map clients that load a style URL, include `endUserId` on the [Get Vector Style](/oem/api-reference/get-style/) request:

<pre>
https://&lt;your-host&gt;:9909/api/v1/styles/base.json?token=&lt;token string&gt;&amp;endUserId=&lt;your-user-id&gt;
</pre>
