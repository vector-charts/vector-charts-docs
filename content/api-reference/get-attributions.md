---
title: "Get Attributions"
weight: 4
menu:
  main:
    parent: "api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/v1/datasets/attributions" title="Get Attributions" request=`GET https://api.vectorcharts.com/api/v1/datasets/attributions`
response=`Status Code: 200 OK
Response Body:
[
  {
    "id": "noaa-enc",
    "shortDescription": "NOAA ENC: United States Nautical Charts",
    "longDescription": "NOAA ENCs are created and published by the United States Government, and cover the contiguous US, Alaska, Hawaii, and US Territories.",
    "sourceUrl": "https://www.nauticalcharts.noaa.gov/charts/noaa-enc.html",
    "dataSourcedAt": 1757941524239,
    "dataProcessedAt": 1757941524239
  },
  {
    "id": "basemap",
    "shortDescription": "Background Data",
    "longDescription": "Background Data sourced from the Natural Earth dataset.",
    "sourceUrl": "https://www.naturalearthdata.com/",
    "dataSourcedAt": 1757941524239,
    "dataProcessedAt": 1757941524239
  }
]` %}}

Retrieve attribution & data provenance for the datasets used by the Vector Charts API.

This can be used in a user interface to display the date that ENC data was loaded for informational purposes.

<b>Query Parameters</b>

N/A. This endpoint does not require authentication.

<b>Response Schema</b>

The endpoint returns an array of objects, each object representing one data source used by Vector Charts. Each data source will have the following fields:

- `id`: A unique textual identifier for the data source.
- `shortDescription`: A one-liner title / short textual description of the data.
- `longDescription`: A longer description of the data.
- `sourceUrl`: A URL to the original data, if available.
- `dataSourcedAt`: The timestamp that the data was downloaded from the source at, in milliseconds since unix epoch.
- `dataProcessedAt`: The timestamp that the data was processed into the Vector Charts system, in milliseconds since unix epoch.
