---
title: "End Users"
weight: 4
menu:
  oem:
    parent: "portal_api_reference"
    identifier: "portal_api_reference_end_users"
---

An end user is a per-seat identity for one vessel, device, or operator that uses chart data through your application. Every end user has its own End User Token. Chart and tile requests send that token in place of an account API token. See [Core API authentication](/oem/api-reference/) and [Cloud authentication](/api-reference/api-authentication/).

The server assigns `endUserId`, a UUID. A human-readable `label` is required when the seat is created, and it can be changed later. List responses include the seat and its licenses, and omit the token. Read the token with [Get End User Token](/oem/portal-api-reference/end-users/get-token/), or replace it with [Regenerate End User Token](/oem/portal-api-reference/end-users/regenerate-token/).

Each account has one default seat, labeled `Account default`. That seat cannot be removed. Removing any other seat revokes its token.

## Cloud and OEM

Account-scoped routes are mounted at `/api/portal/v1/endUsers` on both deployments.

- **Vector Charts Cloud:** `https://cloud.vectorcharts.com`
- **OEM:** `https://<your-host>:9909`

The examples below use the OEM host. Send the same path and body to the Cloud host to manage the signed-in account.

An OEM instance administrator manages another account with the same operations under `/api/portal/v1/admin/accounts/{accountId}/endUsers`. Those routes are listed under [Administration](/oem/portal-api-reference/admin/).

## Authentication

Every route requires a Portal API session token or an account API token in the `Authorization` header. Listing and reading a seat is available to any user on the account. Creating a seat, quoting a new seat, reading or regenerating a token, renaming a seat, and removing a seat require an account administrator.

An End User Token does not authenticate these routes.

## Endpoints

- [List End Users](/oem/portal-api-reference/end-users/list/)
- [Get End User](/oem/portal-api-reference/end-users/get/)
- [Create End User](/oem/portal-api-reference/end-users/create/)
- [Get End User Token](/oem/portal-api-reference/end-users/get-token/)
- [Regenerate End User Token](/oem/portal-api-reference/end-users/regenerate-token/)
- [Update End User](/oem/portal-api-reference/end-users/update/)
- [Remove End User](/oem/portal-api-reference/end-users/delete/)
- [Preview End User](/oem/portal-api-reference/end-users/preview/)
