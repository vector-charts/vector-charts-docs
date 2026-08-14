---
title: "Delete Report"
weight: 4
---

{{% apiEndpointCard method="DELETE" path="/api/v1/user-reports/{id}" title="Delete Report" request=`DELETE https://api.vectorcharts.com/api/v1/user-reports/550e8400-e29b-41d4-a716-446655440000
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
{
    "id": "550e8400-e29b-41d4-a716-446655440000",
    "reportType": "hazard",
    "latitude": 42.36,
    "longitude": -71.05,
    "properties": {},
    "upvoteCount": 3,
    "downvoteCount": 1,
    "isOwner": true,
    "externalUserId": "app-user-abc123",
    "namespace": "public",
    "createdAt": 1718380800000,
    "updatedAt": 1718381100000,
    "expiredAt": null,
    "deletedAt": 1718381100000
}` %}}

Soft-delete a user report. The report remains in the database with `deletedAt` set and is excluded from default list and tile queries.

<b>Authentication</b>

Requires a Bearer token. Only the user who created the report or an admin may delete it.

<b>Path Parameters</b>

- **id**: UUID of the report to delete.

<b>Response</b>

Returns the soft-deleted [User Report]({{< relref "_index.md" >}}) object.

<b>Error Responses</b>

- **400 Bad Request**: Invalid report id.
- **401 Unauthorized**: Token is missing or invalid.
- **403 Forbidden**: Caller is not the report owner or an admin.
- **404 Not Found**: Report does not exist.
- **410 Gone**: Report has already been deleted.

{{% /apiEndpointCard %}}
