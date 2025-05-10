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