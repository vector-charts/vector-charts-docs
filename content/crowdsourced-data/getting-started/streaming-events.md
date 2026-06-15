---
title: "Streaming Events"
weight: 3
menu:
  crowdsourced:
    title: "Streaming Events"
    parent: "getting_started"
    weight: 3
---

The Realtime API delivers JSON event messages over WebSocket when user reports are created, updated, deleted, or expired. This is available on both Vector Charts Cloud and Vector Charts OEM.

## Connection

Connect to:

<pre>
wss://api.vectorcharts.com/api/v1/realtime?token=&lt;token string&gt;
</pre>

On OEM, replace the host with your instance URL (for example, `wss://&lt;your-host&gt;:9909/api/v1/realtime?token=&lt;token string&gt;`).

Authentication uses the same API token as REST endpoints, passed as the `token` query parameter. Unauthenticated connections are rejected.

## Message Format

Each message is a JSON object:

<pre>
{
    "type": "event_user_report",
    "data": {
        "action": "created",
        "report": {
            "id": "550e8400-e29b-41d4-a716-446655440000",
            "reportType": "hazard",
            "position": { "latitude": 42.36, "longitude": -71.05 },
            "properties": {},
            "validVoteCount": 0,
            "invalidVoteCount": 0,
            "externalUserId": "app-user-abc123",
            "createdAt": 1718380800000,
            "updatedAt": 1718380800000,
            "expiresAt": 1718467200000,
            "isExpired": false,
            "isDeleted": false
        }
    },
    "eventAt": 1718380800000
}
</pre>

- **type**: Event namespace. User report events use `event_user_report`.
- **data.action**: One of `created`, `updated`, `deleted`, or `expired`.
- **data.report**: Full report object with vote counts, matching the [User Report API](/crowdsourced-data/user-report-api-reference/) schema.
- **eventAt**: Event timestamp in milliseconds since Unix epoch.

Future event types may use different `type` values on the same WebSocket connection.
