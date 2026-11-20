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

An end user is a per-seat identity for one vessel, device, or operator that uses your application. Every end user has its own End User Token. Create and manage end users with the [End Users](/oem/portal-api-reference/end-users/) Portal API. An instance administrator can manage the end users of any account with the [Administration](/oem/portal-api-reference/admin/) routes.

Send the End User Token on chart and tile requests in place of an account API token, using either method above.

For map clients that load a style URL, pass the End User Token as the `token` query parameter on the [Get Vector Style](/oem/api-reference/get-style/) request:

<pre>
https://&lt;your-host&gt;:9909/api/v1/styles/base.json?token=&lt;end user token&gt;
</pre>

Chart products that require end users reject an account API token with `403 Forbidden` and the code `end_user_required`:

<pre>
{
    "success": false,
    "timestamp": 1736942400000,
    "code": "end_user_required",
    "message": "This account requires an end user token."
}
</pre>

Accounts whose chart products do not require end users can continue to send an account API token. An End User Token is only for Core API chart and tile requests. Calls to the Portal API still use a session token or an account API token. The same account-scoped End User routes are available on Vector Charts Cloud at `https://cloud.vectorcharts.com`.
