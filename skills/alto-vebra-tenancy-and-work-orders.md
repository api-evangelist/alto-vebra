---
name: Run a tenancy and raise property management work orders
description: Create and progress an Alto tenancy, record meter readings and charges, and raise
  maintenance work orders against the property.
api: openapi/alto-api-openapi.json
operations:
- GetOwners
- CreateFileNote
generated: '2026-07-26'
method: generated
source: openapi/alto-api-openapi.json
---

# Run a tenancy and raise property management work orders

The lettings side of Alto. Most operations in this flow carry no `operationId` in the published
spec, so bind by method and path.

Authenticate first — see `alto-vebra-authenticate-and-scope.md`.

## Step 1 — the tenancy

- `GET /tenancies` — list tenancies
- `GET /tenancies/{tenancyId}` — read one
- `GET /inventory/{inventoryId}/tenancies` — tenancies on a property
- `POST /inventory/{inventoryId}/tenancies` — create a tenancy → **`202 Accepted`**
- `PATCH /tenancies/{tenancyId}` — **JSON Patch (RFC 6902)**, not a resource body → `204`

Two things to handle here that differ from the rest of the API:

1. Creating a tenancy returns **202**, not 201. The tenancy is queued, not created. Poll
   `GET /inventory/{inventoryId}/tenancies` for it to appear.
2. `PATCH /tenancies/{tenancyId}` and `PATCH /referrals/{referralId}` take a **JSON Patch
   document**. Every other PATCH in this API takes a resource-shaped body. Sending the wrong
   dialect is a 400.

## Step 2 — the people on it

- `GET /tenancies/{tenancyId}/tenantIds` — tenant contact ids
- `GET /guarantorIds` — guarantor contact ids
- `GET /inventory/{inventoryId}/landlords` — landlords on the property
- `GET /ReferenceChecks` — tenant referencing checks
- `PATCH /ReferenceChecks/{referenceCheckId}` → `202`

Resolve every id through `GetContact` — `GET /contacts/{contactId}`. Alto returns identifier
lists, not embedded objects; there is no expansion or `include` parameter anywhere in this API.

## Step 3 — money and meters

- `POST /tenancies/{tenancyId}/charges` → `201`
- `POST /inventory/{propertyId}/charges` → `201`
- `GET /tenancies/{tenancyId}/meter-readings`
- `POST /tenancies/{tenancyId}/meter-readings` → `201`, `409` if a reading already exists
- `PATCH /tenancies/{tenancyId}/meter-readings/{utilityType}` → `204`

**There is no way to list charges.** Charges can be created against a tenancy or a property and
there is no `GET /charges` operation of any kind. If you need a charge ledger, it is not in this
API — client accounting stays in the Alto application.

## Step 4 — work orders

- `POST /work-orders` → `201`
- `GET /work-orders/{id}` — read one
- `PATCH /work-orders/{id}` → `204`
- `GET /inventory/{inventoryId}/work-orders` — work orders on a property
- `GET /work-orders/{workOrderId}/documents` — documents attached to one
- `GET /suppliers`, `GET /suppliers/{supplierId}`,
  `GET /inventory/{inventoryId}/suppliers` — the contractors

A 400 on `POST /work-orders` commonly means an invalid priority value — the spec's own example
validation message is `"Invalid Priority"`.

## Step 5 — management events

- `GET /management-events` / `POST /management-events` → `201`
- `GET /management-events/{eventId}` / `PATCH /management-events/{eventId}`
- `GET /inventory/{inventoryId}/management-events`

These are the property-management timeline entries — inspections, compliance checks, renewals.

## Safety

Every write in this flow mutates a CRM of record for a real tenancy with legal weight in the
UK. There is **no idempotency key**: a retried `POST /tenancies/{tenancyId}/charges` charges
twice, and a retried `POST /work-orders` dispatches a contractor twice. Confirm before writing,
and reconcile by re-reading rather than by retrying.

## Staying in sync afterwards

Subscribe to `Tenancy.Created`, `Tenancy.Modified`, `Tenancy.ReferencingPassed`,
`Tenancy.Renewed` and `Tenancy.Vacated`. See
`asyncapi/alto-vebra-alto-webhooks-asyncapi.yml`.
