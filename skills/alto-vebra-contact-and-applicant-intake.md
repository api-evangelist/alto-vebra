---
name: Register a contact and record what they are looking for
description: Create or find an Alto contact, attach the people on it, record their marketing
  preferences, and register an applicant requirement so the agency's matching engine can work.
api: openapi/alto-api-openapi.json
operations:
- GetContactsById
- CreateContact
- GetContact
- UpdateContact
- GetPersons
- UpdatePerson
- GetPreferences
- CreateApplicantRequirement
- UpdateApplicantRequirement
- CreateContactRelationship
- GetIntentions
- GetPositions
- GetLeadSources
generated: '2026-07-26'
method: generated
source: openapi/alto-api-openapi.json, https://developers.vebraalto.com/guides/error-codes/
---

# Register a contact and record what they are looking for

A **Contact** in Alto is a party record, not a role. The same contact becomes an applicant, a
vendor, a landlord, a tenant or an owner depending on the relationships and requirements
attached to it. Do not create separate contacts for the same person in different roles.

Authenticate first — see `alto-vebra-authenticate-and-scope.md`.

## Step 1 — look before you create

- `GetContactsById` — `GET /contacts` with the id(s) you already hold
- `GET /contacts/search` — free-text search across all contacts
- `GetAllContacts` — `GET /contacts/all` (paged; see pagination below)

**There is no idempotency key on this API.** A retried create makes a second contact. Always
search first.

## Step 2 — create the contact

`CreateContact` — `POST /contacts` → `201`.

If Alto detects a duplicate it answers **409 Conflict** and puts the URI of the existing
record in one or more `Location` response headers. That is Alto's only duplicate-suppression
mechanism. On a 409, follow the `Location` header and continue with the existing contact — do
**not** retry the create.

Reference data for the fields on this call is enumerated by dedicated operations, and using
them beats guessing:

- `GetIntentions` — `GET /parameters/client-intentions`
- `GetPositions` — `GET /parameters/client-positions`
- `GetClientDisposalStatuses` — `GET /parameters/client-disposal-statuses`
- `GetLeadSources` — `GET /parameters/lead-sources`
- `GetPropertyTypes` — `GET /parameters/property-types`

## Step 3 — the people on the contact

A contact can carry several persons (joint applicants, a couple, a company's named contacts).

- `GetPersons` — `GET /contacts/{contactId}/persons`
- `GetPerson` — `GET /contacts/{contactId}/persons/{personId}`
- `UpdatePerson` — `PATCH /contacts/{contactId}/persons/{personId}`

## Step 4 — marketing preferences before you market

- `GetPreferences` — `GET /contacts/{contactId}/preferences`
- `POST /contacts/{contactId}/preferences` — update marketing preferences

Read preferences before sending anything. This is UK consumer data; the agency, not you,
carries the regulatory obligation, and Alto also exposes
`GetIntegrationOptOutStatus` — `GET /opt-out-status/{linkedType}/{linkedId}` — so an
integration can check whether a subject has opted out of it specifically.

## Step 5 — record the requirement

`CreateApplicantRequirement` — `POST /contacts/{contactId}/applicant-requirements` → `201`.
Amend with `UpdateApplicantRequirement` —
`PATCH /contacts/{contactId}/applicant-requirements/{requirementId}`.

This is what makes the contact an applicant and feeds Alto's applicant/property matching.

## Step 6 — relationships

`CreateContactRelationship` — `POST /contacts/{contactId}/relationship` links two contacts
(for example a tenant to a guarantor, or a vendor to a solicitor). It also answers **409** with
`Location` headers when the relationship already exists. `GetContactRelationship` reads them;
`DeleteContactRelationship` removes one.

## Conventions that bite

- **Pagination**: cursor-based, but the parameter casing varies per operation —
  `next-token`/`max-results`, `nextToken`/`maxResults`, or `NextToken`/`MaxResults`. Read the
  operation's own parameter list; do not assume.
- **Date filters**: `created-from`/`created-to`/`modified-from`/`modified-to` on most
  operations, `createdFrom`/`createdTo`/`modifiedFrom`/`modifiedTo` on a few.
- **Errors**: 400 carries either an RFC 7807-shaped `ProblemDetails` body or an
  `{"errors":[{code,message}]}` body depending on the subsystem. Handle both. See
  `errors/alto-vebra-problem-types.yml`.
- **Bank accounts**: `ListBankAccounts` — `GET /contacts/{contactId}/bank-accounts` — is gated
  behind its own semantic scope `alto/read:contact_bank_accounts`. Leave it out of general
  contact-sync flows.

## Staying in sync afterwards

Subscribe to `Contact.Created` and `Contact.Modified` rather than polling. The notification
carries only ids — re-fetch with `GetContact` using `data.agencyRef` as the `AgencyRef` header.
See `asyncapi/alto-vebra-alto-webhooks-asyncapi.yml`.
