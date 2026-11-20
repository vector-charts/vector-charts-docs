---
title: "Authentication"
weight: 1
menu:
  main:
    parent: "api_reference"
    identifier: "api_reference_authentication"
---

The API uses tokens to manage authentication and track usage for billing. Each API request must be sent with an API token, and there are several methods to do so.

See the [API Tokens](/getting-started/tokens/) section for a step-by-step guide to create a new token.

## Header Authentication

API requests can be authenticated with an `Authorization` header:

<pre>
Authorization: Bearer &lt;token string&gt;
</pre>

## Query Parameter Authentication

Mapping libraries do not usually allow you to directly set request headers for a style. In this case, add the token as a request parameter: `?token=<token string>`.

For example, in Mapbox GL JS:
<pre>
const map = new mapboxgl.Map({
    ...
    style: "https://api.vectorcharts.com/api/v1/styles/base.json?token=&lt;token string&gt;"
});
</pre>

## End Users

An end user is a per-seat identity for one vessel, device, or operator that uses your application. Every end user has its own End User Token. Create and manage end users with the [End Users](/oem/portal-api-reference/end-users/) Portal API. On Vector Charts Cloud that API is served at `https://cloud.vectorcharts.com`.

Send the End User Token on chart and tile requests in place of an account API token, using either method above.

For map clients that load a style URL, pass the End User Token as the `token` query parameter on the [Get Vector Style](/api-reference/get-mvt/) request:

<pre>
https://api.vectorcharts.com/api/v1/styles/base.json?token=&lt;end user token&gt;
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

Accounts whose chart products do not require end users can continue to send an account API token. An End User Token is only for chart and tile requests. Calls to the Portal API still use a session token or an account API token.
