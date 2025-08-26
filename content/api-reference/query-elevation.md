---
title: "Query Elevation"
weight: 4
menu:
  main:
    parent: "api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
draft: true
---





{{% apiEndpointCard method="POST" path="/api/dashboard/:id" title="Get Style" request=`{}` response=`{}` %}}

Look up the elevation along a `LineString` path, using the Vector Charts combined Bathymetry/Terrain height API.

The returned data will contain a number of samples projected along the line. Each sample contains its `latitude`, `longitude`, and `altitude_msl`.

<b>Query Parameters</b>
- **token** <span style="color:red;">(Required)</span>: Vector Charts API token.

<b>Request Body</b>

The request body must be a JSON object with two subfields. `parameters`, holding a number of optional parameters for the lookup, and `geometry`, containing a valid `LineString` geometry or `Feature` containing a `LineString`. 

<b> Optional Parameters </b>
- **numSamples**: Number of samples. If set, the API will always return this many samples. The maximum is 1000. 
- **sampleInterval**: Sample size in meters. Defaults to `1.0`, meaning one sample per meter. If the LineString is longer than 1km (1000 samples), the sample size will be clamped to a maximum of `length / 1000`. `numSamples` takes precedence over `sampleInterval` if set.

<i>Note: To obtain high-resolution elevation across long distances, split your geometry so you can perform the lookup across several requests.</i>


`
{
    "parameters": {},
    "geometry": {...geojson...}
}
`

{

}


{{% /apiEndpointCard %}}