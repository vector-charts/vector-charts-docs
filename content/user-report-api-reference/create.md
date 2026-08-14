---
title: "Create Report"
weight: 2
---

{{% apiEndpointCard method="POST" path="/api/v1/user-reports" title="Create Report" request=`POST https://api.vectorcharts.com/api/v1/user-reports
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
    "upvoteCount": 0,
    "downvoteCount": 0,
    "isOwner": true,
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

Cloud: `https://api.vectorcharts.com` — OEM: `https://<your-host>:9909`

<b>Request Body</b>

- **reportType** <span style="color:red;">(Required)</span>: Report category. Supported values: `hazard`, `accident`, `weather`, `wildlife`.
- **position** <span style="color:red;">(Required)</span>: Object with numeric `latitude` (−90 to 90) and `longitude` (−180 to 180).
- **properties** (Optional): Free-form JSON. Use `description` for free-text notes shown in clients.
- **id** (Optional): Client-supplied UUID version 4. If omitted, the server generates one.
- **externalUserId** (Optional): Opaque user identifier from your application.

<b>Response Schema</b>

Returns the created [User Report]({{< relref "_index.md" >}}) object, including `isOwner: true` for the creating token.

<b>Error Responses</b>

- **400 Bad Request**: Missing `reportType` / `position`, invalid coordinates, or invalid `id`.
- **401 Unauthorized**: Token is missing or invalid.
- **409 Conflict**: A report with the supplied `id` already exists.

{{% /apiEndpointCard %}}
