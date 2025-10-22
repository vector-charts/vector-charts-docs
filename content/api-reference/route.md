---
title: "Compute Route"
weight: 4
menu:
  main:
    parent: "api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/v1/routing/route?token=<token string>" title="Get GeoJSON Tile" request=`POST https://api.vectorcharts.com/api/v1/routing/route?token=299ce9bf4f244300a96f3926240f9c0d
Request Body:
{
    waypoints: [
        [42.338749, -70.986042],
        [42.303464, -70.948277]
    ]
}` response=`
Status Code: 200 OK
Response Body:
{
    "success": true,
    "messages": [],
    "route": [
        [42.340272, -70.985527],
        [42.333293, -70.973511],
        [42.335323, -70.960980],
        [42.335323, -70.947762],
        ...
    ]
}` %}}

<span style="color:#9e6c2e">Feature Preview: This endpoint is restricted to pilot customers. <a href="https://vectorcharts.com/contact-us/">Contact Us</a> if you are interested in access.</span>

Compute a route between a set of two or more waypoints.

The API will internally run a path planning algorithm which attempts to find a safe, optimal route based on a number of constraints (Vessel draft, turning restrictions, etc.)

If successful, the endpoint will return a path as an array of latitude & longitude points.

If the routing fails, the endpoint will return an array of error messages.

<b>Request Body</b>

*The request body should be JSON-encoded.*

- **waypoints** <span style="color:red;">(Required)</span>: An array of two or more input waypoints as `[latitude, longitude]` pairs. The algorithm
will be constrained to route through each of these waypoints sequentially.

<b>Query Parameters</b>

- **token** <span style="color:red;">(Required)</span>: Vector Charts API token.

{{% /apiEndpointCard %}}