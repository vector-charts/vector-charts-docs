---
title: "List User Reports"
weight: 3
menu:
  crowdsourced:
    parent: "user_report_api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/v1/user-reports" title="List User Reports" request=`GET https://api.vectorcharts.com/api/v1/user-reports?limit=50&offset=0
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
{
    "reports": [
        {
            "id": "550e8400-e29b-41d4-a716-446655440000",
            "reportType": "hazard",
            "position": {
                "latitude": 42.36,
                "longitude": -71.05
            },
            "properties": {},
            "validVoteCount": 3,
            "invalidVoteCount": 1,
            "externalUserId": "app-user-abc123",
            "createdAt": 1718380800000,
            "updatedAt": 1718380900000,
            "expiresAt": 1718467200000,
            "isExpired": false,
            "isDeleted": false
        }
    ],
    "total": 1,
    "limit": 50,
    "offset": 0
}` %}}

List all user reports globally, ordered most recent first. Each report includes aggregated vote counts.

<b>Authentication</b>

Requires a Bearer token in the `Authorization` header or a `token` query parameter.

<b>Query Parameters</b>

- **limit** (Optional): Maximum number of reports to return. Defaults to `50`. Capped at `200`.
- **offset** (Optional): Number of reports to skip. Defaults to `0`.
- **includeDeleted** (Optional): If `true`, include soft-deleted reports. Defaults to `false`.
- **includeExpired** (Optional): If `true`, include expired reports. Defaults to `false`.

<b>Response Schema</b>

- **reports**: Array of [User Report](/crowdsourced-data/user-report-api-reference/) objects.
- **total**: Total number of reports matching the filter.
- **limit**: Applied page size.
- **offset**: Applied offset.

<b>Error Responses</b>

- **401 Unauthorized**: Token is missing or invalid.

{{% /apiEndpointCard %}}
