---
title: "Peer Replication"
draft: true
---

User reports can be replicated across multiple OEM instances using a pull-only peer sync. Each instance periodically fetches reports and votes that changed since its last successful sync from configured peer URLs.

Bidirectional replication requires peers to be configured on both sides. Peers only exchange reports in the same **namespace** — set `userReports.namespace` to the same value on each instance that should sync.

## Configuration

In `default.yml` (or environment overrides):

```yaml
userReports:
  namespace: 'public'
  replication:
    enabled: true
    tickIntervalMs: 60000
    token: 'a1b2c3d4-e5f6-4789-a012-3456789abcde'
    peers:
      - name: peer-east
        url: https://peer-east.example.com
      - name: peer-west
        url: https://peer-west.example.com
```

- **enabled**: When false, replication tick is disabled and the internal export endpoint returns 404.
- **tickIntervalMs**: How often to pull from peers (default 60 seconds).
- **token**: Shared UUIDv4 secret. Must match on all peers.
- **peers**: List of remote instances to pull from.
- **namespace**: Namespace to scope reports on this instance (default `public`). Only data in this namespace is exported, imported, or visible via the public API.

Environment variables: `USER_REPORTS_NAMESPACE`, `USER_REPORTS_REPLICATION_ENABLED`, `USER_REPORTS_REPLICATION_TICK_INTERVAL_MS`, `USER_REPORTS_REPLICATION_TOKEN`.

## Internal Export Endpoint

Peers expose changed data at:

<pre>
GET /api/v1/internal/user-reports/replication?since=&lt;timestamp&gt;
Authorization: Bearer &lt;replication token&gt;
</pre>

Query parameters:

- **since** (required): ISO 8601 timestamp or epoch milliseconds. Returns rows with `updated_at` greater than this value.
- **limit** (optional): Page size, default 500, max 2000.
- **cursor** (optional): Report UUID for pagination tie-breaking.
- **voteCursor** (optional): Vote UUID for pagination tie-breaking.

The response includes `reports`, `votes`, `hasMore`, `nextCursor`, and `timestamp`.

Replicated writes do not trigger WebSocket events on the receiving instance.

## Cursor Tracking

Each peer's last successfully ingested timestamp is stored in the `user_report_replication_cursors` table. If a peer pull fails, the cursor is not advanced and the next tick retries from the last successful position.
