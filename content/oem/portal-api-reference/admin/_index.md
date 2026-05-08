---
title: "Admin"
weight: 7
menu:
  oem:
    parent: "portal_api_reference"
    identifier: "portal_api_reference_admin"
---

The Admin endpoints expose server-wide management operations on a Vector Charts OEM instance. They are intended for sysadmin scripts and support tooling, and they are gated by the `isAdmin` flag on the calling user. A user without admin privileges who attempts to call any of these endpoints will receive a `401 Unauthorized` response.

The `isAdmin` flag is visible in the response of the [Get Authenticated User](/oem/portal-api-reference/authentication/whoami/) endpoint, and on each user record returned by [List Team Members](/oem/portal-api-reference/team/list-members/).
