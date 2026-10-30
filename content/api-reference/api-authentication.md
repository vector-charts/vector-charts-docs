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
