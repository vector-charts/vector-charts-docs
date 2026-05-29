---
title: "Administration"
weight: 7
menu:
  oem:
    parent: "portal_api_reference"
    identifier: "portal_api_reference_admin"
---

The Administration endpoints manage the users, accounts, and API tokens of an entire OEM deployment. The rest of the Portal API operates within the caller's own account; these endpoints operate across every account on the instance.

## Admin-Only

All Administration endpoints are mounted under the `/api/portal/v1/admin/` path prefix, and every request is checked for administrator privileges in addition to normal authentication. A valid session or API token that belongs to a non-administrator is rejected with a `403 Forbidden` response.

The default `admin` user provisioned at first startup is an administrator. See [Authentication](/oem/portal-api-reference/authentication/) for how to obtain a token.

## Accounts and Users

An OEM deployment is organized into accounts. Each account owns one or more users and a set of API tokens, and is bound to a chart instance through its `planInstance`. Most administrative tasks follow the same shape: create an account, add users to it, and mint API tokens for those users so their applications can call the Core API.

## Deletion is Asynchronous

Deleting a user or an account is asynchronous. The Portal API returns a `jobId` and enqueues a background job on the chart instance; that job removes the associated data and the record itself. Use the [Jobs](/oem/portal-api-reference/jobs/) endpoints to follow the cleanup job to completion.

## Endpoints

### Users

- [List Users](/oem/portal-api-reference/admin/list-users/)
- [Get User](/oem/portal-api-reference/admin/get-user/)
- [Create User](/oem/portal-api-reference/admin/create-user/)
- [Edit User](/oem/portal-api-reference/admin/edit-user/)
- [Delete User](/oem/portal-api-reference/admin/delete-user/)
- [Impersonate User](/oem/portal-api-reference/admin/impersonate-user/)

### Accounts

- [List Accounts](/oem/portal-api-reference/admin/list-accounts/)
- [Get Account](/oem/portal-api-reference/admin/get-account/)
- [Create Account](/oem/portal-api-reference/admin/create-account/)
- [Edit Account](/oem/portal-api-reference/admin/edit-account/)
- [Delete Account](/oem/portal-api-reference/admin/delete-account/)

### API Tokens

- [List Account API Tokens](/oem/portal-api-reference/admin/list-api-tokens/)
- [Create API Token For User](/oem/portal-api-reference/admin/create-api-token/)
