---
title: "Portal API Overview"
weight: 1
menu:
  oem:
    title: "Overview"
    parent: "portal_api_reference"
    weight: 1
---

The Portal API is used to manage a Vector Charts OEM deployment. It covers users, API tokens, end users, custom charts, styles, background jobs, and instance-wide administration. Account-scoped end user routes are also served on Vector Charts Cloud at `https://cloud.vectorcharts.com/api/portal`.

The Portal API is mounted under the `/api/portal/` path prefix on the OEM server. For an OEM instance running at `https://<your-host>:9909`, the Portal API base URL is:

<pre>
https://&lt;your-host&gt;:9909/api/portal
</pre>

See [Authentication](/oem/portal-api-reference/authentication/) for details on authenticating Portal API requests.

## Categories

- [**Authentication**](/oem/portal-api-reference/authentication/): log in, log out, and inspect the current session.
- [**API Tokens**](/oem/portal-api-reference/api-tokens/): create, list, update, and revoke Core API tokens.
- [**End Users**](/oem/portal-api-reference/end-users/): create per-seat end users, issue End User Tokens, and quote an added seat.
- [**Charts**](/oem/portal-api-reference/charts/): upload S-57 and S-63 charts, list uploads, and manage S-63 permits.
- [**Styles**](/oem/portal-api-reference/styles/): create and manage custom map styles.
- [**Jobs**](/oem/portal-api-reference/jobs/): inspect background jobs and trigger maintenance operations.
- [**Administration**](/oem/portal-api-reference/admin/): manage users, accounts, and API tokens across every account on the instance. Admin-only.
