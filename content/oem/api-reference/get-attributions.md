---
title: "Get Attributions"
weight: 8
menu:
  oem:
    parent: "api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/v1/datasets/attributions" title="Get Attributions" request=`GET https://<your-host>:9909/api/v1/datasets/attributions` response=`Status Code: 200 OK
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

Returns attribution and provenance metadata for the datasets bundled with the OEM instance. Use this to display source credits and data freshness in a user interface.

<b>Authentication</b>

This endpoint does not require authentication.

<b>Response Schema</b>

The endpoint returns an array of dataset records.

- `id`: A unique identifier for the dataset.
- `shortDescription`: A one-line title for the dataset.
- `longDescription`: A longer description of the dataset.
- `sourceUrl`: A URL to the original data, when one exists.
- `dataSourcedAt`: Timestamp when the data was downloaded from the source, in milliseconds since unix epoch.
- `dataProcessedAt`: Timestamp when the data was processed into the OEM instance, in milliseconds since unix epoch.

{{% /apiEndpointCard %}}
