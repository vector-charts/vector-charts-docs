---
title: "Create User Report"
weight: 2
menu:
  crowdsourced:
    parent: "user_report_api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/v1/user-reports" title="Create User Report" request=`POST https://api.vectorcharts.com/api/v1/user-reports
Authorization: Bearer <token>
Content-Type: application/json

{
    "id": "550e8400-e29b-41d4-a716-446655440000",
    "reportType": "hazard",
    "position": {
        "latitude": 42.36,
        "longitude": -71.05
    },
    "properties": {
        "description": "Shallow area reported"
    },
    "externalUserId": "app-user-abc123"
}` response=`Status Code: 201 Created
Response Body:
{
    "id": "550e8400-e29b-41d4-a716-446655440000",
    "reportType": "hazard",
    "latitude": 42.36,
    "longitude": -71.05,
    "properties": {
        "description": "Shallow area reported"
    },
    "validVoteCount": 0,
    "invalidVoteCount": 0,
    "externalUserId": "app-user-abc123",
    "namespace": "public",
    "createdAt": 1718380800000,
    "updatedAt": 1718380800000,
    "expiredAt": null,
    "deletedAt": null
}` %}}

Create a new crowdsourced user report at the given position.

<b>Authentication</b>

Requires a Bearer token in the `Authorization` header or a `token` query parameter. On OEM, use a token from your instance's [Admin API](/oem/portal-api-reference/api-tokens/).

<b>Base URL</b>

Cloud: `https://api.vectorcharts.com` — OEM: `https://&lt;your-host&gt;:9909`

<b>Request Body</b>

- **reportType** <span style="color:red;">(Required)</span>: Category string.
- **position** <span style="color:red;">(Required)</span>: Object with `latitude` and `longitude` (WGS84 decimal degrees).
- **id** (Optional): Client-supplied UUID version 4. When omitted, the server assigns one. Useful for offline-first clients that pre-generate IDs before sync.
- **properties** (Optional): Arbitrary JSON metadata (for example, a description or heading).
- **externalUserId** (Optional): Opaque user identifier from your application. Not used for authorization.

<b>Response Schema</b>

Returns a [User Report](/crowdsourced-data/user-report-api-reference/) object with vote counts set to zero.

<b>Error Responses</b>

- **400 Bad Request**: Invalid `reportType`, position, or `id` is not a valid UUIDv4.
- **401 Unauthorized**: Token is missing or invalid.
- **409 Conflict**: A report with the supplied `id` already exists.

{{% /apiEndpointCard %}}
