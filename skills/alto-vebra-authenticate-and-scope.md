---
name: Authenticate to Alto and scope a call to one agency
description: Obtain a Bearer token from the Alto token endpoint and attach the AgencyRef header
  that scopes every call to a single estate agency. Every other Alto skill depends on this one.
api: openapi/alto-api-openapi.json
operations:
- GetContactsById
generated: '2026-07-26'
method: generated
source: https://developers.vebraalto.com/guides/authenticating-your-requests/, https://developers.vebraalto.com/guides/error-codes/
---

# Authenticate to Alto and scope a call to one agency

Alto needs **two** credentials on every request, not one. Getting either wrong fails
differently, and the difference is the fastest way to diagnose a problem.

## Before you start

You cannot obtain credentials programmatically. An integration must already be registered in
Alto Connect (`https://connect.vebraalto.com/connect`) under an existing contract with Vebra
Solutions, and an individual agency must have activated it. The client id, client secret and
per-agency `AgencyRef` all arrive by email. If you do not have all three, stop — there is no
self-serve path.

## Step 1 — get a Bearer token

`POST https://api.alto.zoopladev.co.uk/token` (this is the sandbox host, and it is the only
token URL Alto publishes).

- `Content-Type: application/x-www-form-urlencoded`
- `Authorization: Basic <base64(clientId + ":" + clientSecret)>`
- body: `grant_type=client_credentials`

Cache the returned token for its stated lifetime. Do not request a new token per call.

## Step 2 — call with both headers

Every subsequent request carries:

- `Authorization: Bearer <token>`
- `AgencyRef: <the agency reference for the agency you are acting for>`

`AgencyRef` is declared as a required header parameter on 110 of the 112 published operations.
It is the multi-tenant boundary: identifiers in Alto are integers that are unique only inside
one agency, so the same `contactId` in two agencies is two different people. Never carry an
identifier across agencies.

Verify the pair works with a cheap read before doing anything else:

- `GetContactsById` — `GET /contacts` (requires scope `alto/route:get-contacts`)

## Step 3 — read the failure correctly

| Status | Meaning | What to do |
|---|---|---|
| 401 | Missing or expired bearer token | Re-run step 1. Check the `Authorization` header is present. |
| 403 | Invalid scope **or** AgencyRef for the request | The token is fine. Either the `AgencyRef` is wrong for this data, or the integration's permissions do not cover the endpoint — email `connectsupport@altosoftwaregroup.co.uk` with the Integration Name. |
| 400 / 404 | URL or query parameters wrong | Check the path against the API reference and confirm required query parameters are present. |

Alto uses 401 and 403 consistently and meaningfully. Treating them as interchangeable is the
single most common integration mistake against this API.

## Scopes

101 distinct scope strings are published in the operation descriptions in the form
`Required scope: alto/read:contacts`. Two generations coexist: six semantic scopes
(`alto/read:contacts`, `alto/read:appointments`, `alto/read:leads`, `alto/update:leads`,
`alto/read:contact_bank_accounts`, `alto/write:appointments_general`,
`alto/write:appointments_viewings`) and 95 mechanical per-route scopes
(`alto/route:get-inventory-inventoryid-tenancies`). They are **not** declared in the
`securitySchemes` object, so a generated client will not know they exist. The full map lives in
`scopes/alto-vebra-scopes.yml`.

Treat `alto/read:contact_bank_accounts` as privileged — it reads landlord and tenant bank
details. Do not request it unless the flow genuinely needs it.

## Zoopla is a separate estate

The Zoopla Leads, Premium Listing and WFP APIs use a different authorization server
(`https://services-auth.services.zoopla.co.uk/oauth2/token`), different scopes
(`leads/list:applicant-leads`, `leads/list:appraisal-leads`, `api/api_access`) and no
`AgencyRef`. An Alto token will not work against `services.zoopla.co.uk` and vice versa.
