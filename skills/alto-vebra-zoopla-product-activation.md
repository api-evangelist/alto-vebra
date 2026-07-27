---
name: Activate a Zoopla Premium Listing or Weekly Featured Property
description: Buy and confirm a Zoopla portal upgrade against a listing, handling the
  accepted-then-poll contract and the numeric error register.
api: openapi/zoopla-premium-listing-activations-openapi.json
operations:
- POST /products/premium-listings
- GET /products/premium-listings/{uuid}
- PATCH /products/premium-listings/{uuid}
- POST /products/weekly-featured-properties
- GET /products/weekly-featured-properties/{uuid}
generated: '2026-07-26'
method: generated
source: openapi/zoopla-premium-listing-activations-openapi.json, openapi/zoopla-weekly-featured-property-openapi.json,
  https://developers.zoopla.co.uk/docs/premium-listings-error-codes-register
---

# Activate a Zoopla Premium Listing or Weekly Featured Property

**These operations spend the customer's money.** Premium Listings and Weekly Featured
Properties are billable Zoopla products activated against a listing under the agency's
contract. Never call them speculatively, never retry blindly, and confirm intent before every
POST.

## Authentication

Different estate from Alto. `POST https://services-auth.services.zoopla.co.uk/oauth2/token`
with `Authorization: Basic <base64(client_id:client_secret)>`,
`grant_type=client_credentials`, `scope=api/api_access`. The token lives 3600 seconds — cache
it. There is no `AgencyRef` on this side. Zoopla ships the `client_secret` PGP-encrypted to a
public key you supply.

## Step 1 — check the listing will pass the quality gate

Zoopla enforces editorial policy as API errors. Verify before you spend:

| Product | Requirement | Failure code |
|---|---|---|
| Premium Listing | full description ≥ 200 characters | 1011007 |
| Premium Listing | at least 3 images assigned | 1011008 |
| Premium Listing | custom details ≤ 640 kb | 1011009 (HTTP 413) |
| Weekly Featured Property | at least 1 image assigned | 2011007 |
| Weekly Featured Property | listing is in the UK | 2011008 |

If the listing comes from Alto, fix it there first — see
`alto-vebra-property-to-listing.md`.

## Step 2 — activate

- `POST /products/premium-listings` → **`202 Accepted`** (queued) or **`303 See Other`**
  (an equivalent activation already exists — follow the redirect, do not retry)
- `POST /products/weekly-featured-properties` → same contract

A 202 does **not** mean the product is live. The activation is queued and can still fail
downstream in the Premium Listings Processor (service 102), whose errors surface as 102xxxx
codes on a later read — never on the original POST.

## Step 3 — poll for the terminal state

- `GET /products/premium-listings/{uuid}`
- `GET /products/weekly-featured-properties/{uuid}`

`404` here is deliberately ambiguous: it means "does not exist **or** you do not have access
to it". Do not treat it as proof the activation failed.

Collection reads: `GET /products/premium-listings` and
`GET /products/weekly-featured-properties` return everything the caller can see.

## Step 4 — amend highlights (Premium Listing only)

`PATCH /products/premium-listings/{uuid}` → `202`. Constraints from the register:

- Only an **active** listing can be updated — expiry in the future and status `ACTIVATED`
  (1011043).
- Only one update may be in flight at a time (1011044, HTTP 409). Wait, then retry.
- Invalid highlights are rejected with 1011905.

## Reading the errors

The envelope is `{"errors":[{"code": <7-digit int>, "reason": "<text>"}]}`. The code decomposes
as service (3) + severity (1) + custom code (3): `1011003` is service 101 (Premium Listings
API), severity 1, code 003. Route on the numeric code, not on the HTTP status — several
distinct failures share a 400. The full transcribed register is in
`errors/alto-vebra-error-codes.yml`.

Codes worth handling explicitly:

- `1011003` / `1011004` — a pending or activated premium listing already exists for this
  listingId. This is the closest thing to idempotency protection you get. Stop.
- `1011051` / `1011055` — listingId not found, or does not match the one provided.
- `1011061` — cannot match a `customerListingId` to a Zoopla `listingId`. Configuration, not
  code: the client has no sources assigned (1011064) or the mapping is missing.
- `1011065` — `listingId` and `customerListingId` must not both be set.
- `1011901` — the client does not have access to that listing.
- `1021006` — the contract does not have premium features activated. Commercial, not technical.

## No sandbox

Zoopla publishes no test environment, no test client and no test listing id for these APIs.
Every call in this skill hits production. Treat that as the governing constraint on how you
build and test the integration.
