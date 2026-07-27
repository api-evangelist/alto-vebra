---
name: Turn a lead into a booked viewing or valuation
description: Pull leads from Zoopla or Alto, accept and update them, then book the viewing
  appointment or create the appraisal that follows.
api: openapi/alto-api-openapi.json
operations:
- GetById
- UpdateLead
- CreateAppraisal
- PatchAppraisal
- GetLeadSources
generated: '2026-07-26'
method: generated
source: openapi/alto-api-openapi.json, openapi/zoopla-leads-api-openapi.json, https://developers.zoopla.co.uk/leads/docs/push-service
---

# Turn a lead into a booked viewing or valuation

This flow crosses both estates in this repo. Leads originate on the Zoopla portal and land in
Alto; the appointment and the appraisal are written back into Alto.

Authenticate first — see `alto-vebra-authenticate-and-scope.md`. Note that the Zoopla side uses
a *different* token endpoint and no `AgencyRef`.

## Step 1 — get the leads

Two independent sources, and you should prefer the event-driven one:

**Alto leads**
- `GET /leads` — paginated list (scope `alto/read:leads`)
- `GetById` — `GET /leads/{leadId}`
- `POST /leads` — create a lead → `201`, `409` if one already exists for the source identifier
  in the request, `422` if it cannot be created for the specified branch
- `UpdateLead` — `PATCH /leads/{leadId}` (scope `alto/update:leads`)
- `GetLeadSources` — `GET /parameters/lead-sources`

**Zoopla portal leads** (`openapi/zoopla-leads-api-openapi.json`)
- `GET /applicant-leads` — buyers and renters (scope `leads/list:applicant-leads`)
- `GET /appraisal-leads` — sellers and landlords wanting a valuation (scope
  `leads/list:appraisal-leads`)

Both Zoopla operations default to the **last 24 hours** and accept `from-time`/`to-time`;
Zoopla retains leads for **30 days**. If the customer has more than one branch, brand, company
or group, one of `branch-id`/`brand-id`/`company-id`/`group-id` becomes required.

A 429 from the Zoopla leads API means "service busy", not a quota breach. Wait and retry, and
cache the access token for its full 3600-second lifetime instead of re-authenticating per call.

Prefer the **push service** over polling: it delivers the same payload in real time and retries
for 24 hours. See `asyncapi/alto-vebra-zoopla-leads-push-asyncapi.yml`.

## Step 2 — attach the lead to a party

Find or create the Contact and record the requirement — see
`alto-vebra-contact-and-applicant-intake.md`. Search before creating; there is no idempotency
key anywhere in this flow.

## Step 3 — book the viewing

- `POST /appointments/viewings` — create a viewing appointment (scope
  `alto/write:appointments_viewings`)
- `PATCH /appointments/viewings/{appointmentId}` — amend an existing viewing
- `POST /appointments/general` — a non-viewing appointment (scope
  `alto/write:appointments_general`)
- `PATCH /appointments/general/{appointmentId}` — amend it
- `GET /appointments/negotiators` — a negotiator's diary in a time range, to find a slot
- `GET /appointments/{appointmentId}/{instanceId}` — read one instance of a recurring
  appointment
- `GET /parameters/appointment-subtypes` — valid general-appointment sub-types

Appointments are recurring-capable: an appointment is addressed by `appointmentId` **and**
`instanceId`. Do not assume one id is enough.

## Step 4 — or raise the valuation

For an appraisal (valuation) lead:

- `GET /appointments/valuations` — valuations booked in a time range
- `CreateAppraisal` — `POST /appraisals` → `201`
- `PatchAppraisal` — `PATCH /inventory/{propertyId}/appraisal` → `204`

Alto models valuation as a human appointment plus an appraisal record. There is **no AVM and
no automated valuation endpoint** in this API — do not look for one.

## Step 5 — leave a trail

`CreateFileNote` — `POST /file-notes` → `201`; `PatchFileNote`, `GetFileNote`,
`SearchFileNotes` — `GET /file-notes/search`. Alto publishes a specific guide for storing email
conversations in file notes:
`https://developers.vebraalto.com/guides/guide-for-storing-email-conversations-in-filenotes/`.

## Staying in sync afterwards

Subscribe to `Lead.Received`, `Lead.Accepted`, `Lead.Modified`, `Appointment.Created` and
`Appointment.Modified`. Notifications carry ids only — re-fetch with `GetById`. Delivery order
is not guaranteed and duplicates are expected; de-duplicate on the CloudEvents `id`.
