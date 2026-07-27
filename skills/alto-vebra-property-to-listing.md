---
name: Take a property from inventory record to marketed listing
description: Create an Alto inventory item, attach the owner, add media, then update the
  marketing listing summary and rooms that feed the portals.
api: openapi/alto-api-openapi.json
operations:
- PatchListingSummary
- PatchListingRooms
- GetPropertyTypes
- GetOwners
generated: '2026-07-26'
method: generated
source: openapi/alto-api-openapi.json
---

# Take a property from inventory record to marketed listing

Alto separates two things that most people conflate:

- **Inventory** — the property as the agency holds it (`/inventory`)
- **Listing** — the marketing projection of that property (`/listing/property/{propertyId}`)

Portal distribution happens on the Listing side. Getting an inventory record right does not
make a property appear anywhere.

Authenticate first — see `alto-vebra-authenticate-and-scope.md`.

## Step 1 — find or create the inventory item

- `GET /inventory/search` — search inventory items (scope `alto/route:get-inventory-search`)
- `GET /inventory/filter` — structured filter
- `GET /inventory/items` — fetch several by id
- `GET /inventory/{inventoryId}` — fetch one
- `POST /inventory/new` — create one → `201` (scope `alto/route:post-inventory-new`)

`GetPropertyTypes` — `GET /parameters/property-types` — enumerates the valid property types.
There is no idempotency key on `POST /inventory/new`; search before creating.

## Step 2 — attach the owner

`POST /inventory/{inventoryId}/owner` associates an existing Contact with the property as its
owner → `201`, or `409` if the association already exists. `GetOwners` — `GET /owners` — lists
owners; `GET /inventory/{inventoryId}/landlords` reads the landlord side for a lettings
property.

## Step 3 — add media

- `POST /media-item` — create a media item
- `POST /inventory/{inventoryId}/media-link` — create a VirtualTour or WebLink item
- `DELETE /media-item/{mediaItemId}` — remove one

Media count matters downstream: Zoopla will refuse a Premium Listing activation on a listing
with fewer than 3 images, and a Weekly Featured Property with fewer than 1. See
`errors/alto-vebra-error-codes.yml` codes 1011008 and 2011007.

## Step 4 — write the marketing listing

- `PatchListingSummary` — `PATCH /listing/property/{propertyId}/summary` → `204`
- `PatchListingRooms` — `PATCH /listing/property/{propertyId}/rooms` → `204`

Both return `204 No Content`, so re-read to confirm state:

- `GET /listing/property/{propertyId}` — the listing
- `GET /listing/property/{propertyId}/images` — image metadata
- `GET /listing/property/{propertyId}/images/{imageId}` — one image
- `GET /listing/filter` / `GET /listing/property/items` — listing collections

A full description of at least 200 characters is required before Zoopla will accept a Premium
Listing activation for this property (code 1011007). Write the summary with that in mind.

## Step 5 — keys, documents and notes

- `POST /inventory/{inventoryId}/keyset`, `PATCH .../keyset/{keySetId}`,
  `DELETE .../keyset/{keySetId}`, `GET /inventory/{inventoryId}/keysets`
- `GET /inventory/{inventoryId}/documents`, `POST /documents/post`,
  `GET /documents/{documentId}/content`
- `GetFileNotesByProperty` — `GET /inventory/{propertyId}/file-notes`;
  `CreateFileNote` — `POST /file-notes`

## Conventions that bite

- `inventoryId` and `propertyId` are the **same identifier** with two different parameter names
  across the API. `PATCH /inventory/{propertyId}/appraisal` and
  `GET /inventory/{inventoryId}` address the same record.
- `PATCH /inventory/{inventoryId}` returns `204`, so nothing comes back — plan a re-read.
- Ids are agency-scoped integers. There is no global property identifier: the UK has no MLS and
  no RESO Universal Property Identifier.
- Nothing in either Alto's or Zoopla's contract publishes the mapping between an Alto
  `propertyId` and a Zoopla `listingId`. The Zoopla side resolves a `customerListingId` through
  its Listing Matching Service; expect that seam to need configuration, not code.

## Staying in sync afterwards

Subscribe to `Property.Created`, `Property.Modified` and `Property.MarketingInformationSent`
instead of polling `/inventory`. See `asyncapi/alto-vebra-alto-webhooks-asyncapi.yml`.
