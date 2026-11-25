---
title: "Lookup Elevation in Polygons"
weight: 9.3
menu:
  oem:
    parent: "api_reference"
    name: "Lookup polygons"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/v2/elevation/lookup/polygons" title="Lookup Elevation in Polygons" request=`POST https://<your-host>:9909/api/v2/elevation/lookup/polygons
Authorization: Bearer YOUR_API_TOKEN
Content-Type: application/json

{
  "polygons": [
    {
      "coordinates": [
        { "latitude": 37.80, "longitude": -122.50 },
        { "latitude": 37.80, "longitude": -122.46 },
        { "latitude": 37.84, "longitude": -122.46 },
        { "latitude": 37.84, "longitude": -122.50 }
      ],
      "xSamples": 2,
      "ySamples": 2
    }
  ],
  "options": { "filterOutputReferences": ["MSL"] }
}` response=`Status Code: 200 OK
Content-Type: application/json

{
  "metadata": { "unit": "meters" },
  "data": [
    {
      "locations": [
        { "latitude": 37.81, "longitude": -122.49 },
        { "latitude": 37.81, "longitude": -122.47 },
        { "latitude": 37.83, "longitude": -122.49 },
        { "latitude": 37.83, "longitude": -122.47 }
      ],
      "elevations": [
        { "reference": "MSL", "values": [-12.0, -8.5, 4.0, -6.0] }
      ],
      "failures": []
    }
  ]
}` %}}

Samples a grid inside one or more polygon rings. `data` is an array with one entry per polygon.

The grid is `xSamples` by `ySamples` cell centers on the ring's longitude/latitude bounding box. Longitude varies fastest, and rows run from south to north. Centers on the boundary or outside the ring are omitted, so `locations` can be shorter than `xSamples * ySamples`. Do not repeat the first coordinate at the end of the ring.

See [Elevation](/oem/api-reference/elevation/) for units, depth sign, limits, and errors. The numbers above show the JSON shape.

<b>Authentication</b>

Bearer token or `token` query parameter. See [Authentication](/oem/api-reference/).

<b>Request Body</b>

- **polygons** <span style="color:red;">(Required)</span>: 1 to 1000 shapes.
  - **coordinates**: At least three positions forming a simple ring with area. No consecutive duplicates, and do not close the ring by repeating the first position.
  - **xSamples** (Optional): Integer from 2 through 10000. Default 10. Columns across longitude.
  - **ySamples** (Optional): Integer from 2 through 10000. Default 10. Rows across latitude.
- **options**: Same fields as [Lookup points](/oem/api-reference/elevation-lookup-points/).

An omitted sample count counts as 10 toward the request budget of 100000 samples. The budget uses `xSamples * ySamples` even when some cells fall outside the ring.

<b>Response</b>

`metadata.unit` is `meters` or `feet`. Each `data[]` entry has `locations`, `elevations`, and `failures`. Band `values` line up with `locations`.

{{% /apiEndpointCard %}}
