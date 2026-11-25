---
title: "Convert Altitude in Polygons"
weight: 9.6
menu:
  oem:
    parent: "api_reference"
    name: "Convert polygons"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/v2/elevation/convert/polygons" title="Convert Altitude in Polygons" request=`POST https://<your-host>:9909/api/v2/elevation/convert/polygons
Authorization: Bearer YOUR_API_TOKEN
Content-Type: application/json

{
  "initialAltitude": {
    "value": 10,
    "unit": "meters",
    "reference": "AboveSeafloor"
  },
  "targetPolygons": [
    {
      "coordinates": [
        { "latitude": 37.80, "longitude": -122.50 },
        { "latitude": 37.80, "longitude": -122.46 },
        { "latitude": 37.84, "longitude": -122.48 }
      ],
      "xSamples": 2,
      "ySamples": 2
    }
  ]
}` response=`Status Code: 200 OK
Content-Type: application/json

{
  "metadata": {
    "unit": "meters",
    "constantAltitude": {
      "value": 10,
      "unit": "meters",
      "reference": "AboveSeafloor"
    }
  },
  "data": [
    {
      "locations": [
        { "latitude": 37.81, "longitude": -122.49 },
        { "latitude": 37.81, "longitude": -122.47 }
      ],
      "altitudes": [
        { "reference": "MSL", "values": [-2.0, -6.0] },
        { "reference": "HAE", "values": [-34.2, -38.2] },
        { "reference": "AGL", "values": [-2.0, -6.0] },
        { "reference": "AboveSeafloor", "values": [10, 10] }
      ],
      "failures": []
    }
  ]
}` %}}

Holds one altitude and converts it on the grid inside each polygon. `data` is an array with one entry per polygon. The grid rules match [Lookup polygons](/oem/api-reference/elevation-lookup-polygons/). This triangle's 2 by 2 grid has four cell centers on the bounding box, and only the two southern centers fall inside the ring.

`AboveSeafloor` in the example is the held reference, so that band stays 10 and does not sample. The other bands are that 10 m clearance expressed in each reference.

See [Convert points](/oem/api-reference/elevation-convert-points/) for `initialAltitude` and `constantAltitude`. See [Elevation](/oem/api-reference/elevation/) for limits and errors. The numbers above show the JSON shape.

<b>Authentication</b>

Bearer token or `token` query parameter. See [Authentication](/oem/api-reference/).

<b>Request Body</b>

- **initialAltitude** <span style="color:red;">(Required)</span>: `{ value, unit, reference }`.
- **targetPolygons** <span style="color:red;">(Required)</span>: 1 to 1000 rings. Each needs at least three coordinates and optional `xSamples` and `ySamples` (each 2 through 10000, default 10).
- **options**: Same as [Convert points](/oem/api-reference/elevation-convert-points/).

{{% /apiEndpointCard %}}
