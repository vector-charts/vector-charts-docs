---
title: "Search Query"
weight: 4
draft: true
menu:
  main:
    parent: "api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/v1/enc_query" title="Search Query" request=`
Request URL:
POST https://api.vectorcharts.com/api/v1/enc_query
{
    "position": {
        "latitude": 42.33579873875422,
        "longitude": -70.93892104223606
    },
    "radius": 200
}
` response=`
{
    "results": [
        {
            "id": 6573708,
            "parentId": "US5BOSCE",
            "layerId": "CBLARE",
            "layerName": "Cable area",
            "position": [
                42.31748357594915,
                -70.93106634453447
            ],
            "geometry": {
                "type": "Polygon",
                "coordinates": [
                    [...]
                ]
            },
            "attributes": {
                "objectName": null
            },
            "bbox": [
                [
                    -70.95,
                    42.3
                ],
                [
                    -70.913938,
                    42.3365896
                ]
            ]
        }
    ]
}
` %}}

Perform a spatial search around a position and radius, and return the most relevant nautical chart data in that area. 

Relevance is determined based on proximity and size of the object.

Results are returned as an array of objects with name & other metadata and geometry as GeoJSON.

Warning: This endpoint is a WIP and is subject to change.

{{% /apiEndpointCard %}}