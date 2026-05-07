---
title: "Portal API Overview"
weight: 1
menu:
  oem:
    title: "Overview"
    parent: "portal_api_reference"
    weight: 1
---

The Portal API is used to manage a Vector Charts OEM deployment. It covers users, API tokens, custom charts, styles, and background jobs.

The Portal API is mounted under the `/api/portal/` path prefix on the OEM server. For an OEM instance running at `https://<your-host>:9909`, the Portal API base URL is:

<pre>
https://&lt;your-host&gt;:9909/api/portal
</pre>

See [Authentication](/oem/portal-api-reference/authentication/) for details on authenticating Portal API requests.

## Categories

- [**Authentication**](/oem/portal-api-reference/authentication/): log in, log out, and inspect the current session.
- [**API Tokens**](/oem/portal-api-reference/api-tokens/): create, list, update, and revoke Core API tokens.
- [**Charts**](/oem/portal-api-reference/charts/): upload S-57 and S-63 charts, list uploads, and manage S-63 permits.
- [**Styles**](/oem/portal-api-reference/styles/): create and manage custom map styles.
- [**Jobs**](/oem/portal-api-reference/jobs/): inspect background jobs and trigger maintenance operations.
- [**Team**](/oem/portal-api-reference/team/): invite team members, list members, and change your password.
- [**Admin**](/oem/portal-api-reference/admin/): server-wide management operations for admin users.
