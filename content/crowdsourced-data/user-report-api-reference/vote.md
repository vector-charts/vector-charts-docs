---
title: "Vote on User Report"
weight: 6
menu:
  crowdsourced:
    parent: "user_report_api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/v1/user-reports/{id}/votes" title="Vote on User Report" request=`POST https://api.vectorcharts.com/api/v1/user-reports/550e8400-e29b-41d4-a716-446655440000/votes
Authorization: Bearer <token>
Content-Type: application/json

{
    "vote": "valid",
    "externalUserId": "app-user-abc123"
}` response=`Status Code: 200 OK
Response Body:
{
    "id": "550e8400-e29b-41d4-a716-446655440000",
    "reportType": "hazard",
    "latitude": 42.36,
    "longitude": -71.05,
    "properties": {},
    "validVoteCount": 4,
    "invalidVoteCount": 1,
    "externalUserId": "app-user-abc123",
    "namespace": "public",
    "createdAt": 1718380800000,
    "updatedAt": 1718381000000,
    "expiredAt": null,
    "deletedAt": null
}` %}}

Vote that a user report is valid or invalid. Each authenticated user may have at most one vote per report; submitting again updates the existing vote.

<b>Authentication</b>

Requires a Bearer token in the `Authorization` header or a `token` query parameter.

<b>Path Parameters</b>

- **id**: UUID of the report to vote on.

<b>Request Body</b>

- **vote** <span style="color:red;">(Required)</span>: Either `valid` or `invalid`.
- **externalUserId** (Optional): Opaque user identifier from your application.

<b>Response</b>

Returns the updated [User Report](/crowdsourced-data/user-report-api-reference/) object with refreshed vote counts. Individual vote rows are not returned.

<b>Error Responses</b>

- **400 Bad Request**: Invalid report id or vote value.
- **401 Unauthorized**: Token is missing or invalid.
- **404 Not Found**: Report does not exist.
- **410 Gone**: Report has been deleted or expired.

{{% /apiEndpointCard %}}
