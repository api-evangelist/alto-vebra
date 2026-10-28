# Alto (Vebra / Zoopla)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Alto — formerly Vebra Alto, and still trading through vebra.com — is the United Kingdom's most widely deployed estate agency CRM, used by more than 6,000 sales and lettings agency branches to run valuations, listings, applicant matching, offers, sales and lettings progression, tenancies, property management, work orders and client accounting. It is owned by Houseful Limited, the parent of the Zoopla portal, which places Alto at the exact chokepoint of the UK residential market — the country has no MLS, so listings reach Rightmove and Zoopla through agency CRM software rather than a shared cooperative database, and Alto is the largest of those pipes. Its API posture is genuinely strong on the contract side and closed on the access side: Alto publishes an open, unauthenticated developer portal at developers.vebraalto.com carrying a complete OpenAPI 3.0.4 document (95 paths, 112 operations across 27 resource families) served verbatim from api-docs.vebraalto.com, alongside 26 documented CloudEvents 1.0 webhook event types and 101 published OAuth scope strings. But credentials are partner-only — a developer must register an integration in Alto Connect, be bound by an existing contract with Vebra Solutions, and then wait for an individual agency to activate the integration and issue an AgencyRef before a single call can be made. Sibling Zoopla portal product APIs (Leads, Premium Listing Activations, Weekly Featured Property) are documented publicly at developers.zoopla.co.uk with downloadable specs but are likewise restricted to contracted Zoopla agency customers. There is no SDK, CLI, Postman collection, MCP server or status page anywhere in the estate, and no RESO Web API or Data Dictionary certification exists — RESO is a North American NAR-driven standard with no UK counterpart. Alto publishes no open data; the UK's open property layer sits with HM Land Registry and Ordnance Survey, not with the private CRM duopoly feeders.

**Areas:** Real Estate · United Kingdom · PropTech · Property Listings · CRM · Property Management · Rentals · Conveyancing · Estate Agency · Tenancy · Webhook · Event

## Alto (Vebra / Zoopla) on APIs.io

Everything profiled for Alto (Vebra / Zoopla) is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/alto-vebra/](https://apis.io/providers/alto-vebra/)** — or go straight to one of the APIs or properties below.

### APIs (29)

- [Alto (Vebra / Zoopla) Appointments API](https://apis.io/apis/alto-vebra/alto-vebra-appointments-api/) — The Appointments API from Alto (Vebra / Zoopla) — 7 operation(s) for appointments.
- [Alto (Vebra / Zoopla) Appraisals API](https://apis.io/apis/alto-vebra/alto-vebra-appraisals-api/) — The Appraisals API from Alto (Vebra / Zoopla) — 2 operation(s) for appraisals.
- [Alto (Vebra / Zoopla) Branches API](https://apis.io/apis/alto-vebra/alto-vebra-branches-api/) — The Branches API from Alto (Vebra / Zoopla) — 2 operation(s) for branches.
- [Alto (Vebra / Zoopla) Charges API](https://apis.io/apis/alto-vebra/alto-vebra-charges-api/) — The Charges API from Alto (Vebra / Zoopla) — 2 operation(s) for charges.
- [Alto (Vebra / Zoopla) Clients API](https://apis.io/apis/alto-vebra/alto-vebra-clients-api/) — The Clients API from Alto (Vebra / Zoopla) — 1 operation(s) for clients.
- [Alto (Vebra / Zoopla) Contacts API](https://apis.io/apis/alto-vebra/alto-vebra-contacts-api/) — The Contacts API from Alto (Vebra / Zoopla) — 13 operation(s) for contacts.
- [Alto (Vebra / Zoopla) Documents API](https://apis.io/apis/alto-vebra/alto-vebra-documents-api/) — The Documents API from Alto (Vebra / Zoopla) — 5 operation(s) for documents.
- [Alto (Vebra / Zoopla) Inventory API](https://apis.io/apis/alto-vebra/alto-vebra-inventory-api/) — The Inventory API from Alto (Vebra / Zoopla) — 10 operation(s) for inventory.
- [Alto (Vebra / Zoopla) Landlords API](https://apis.io/apis/alto-vebra/alto-vebra-landlords-api/) — The Landlords API from Alto (Vebra / Zoopla) — 2 operation(s) for landlords.
- [Alto (Vebra / Zoopla) Leads API](https://apis.io/apis/alto-vebra/alto-vebra-leads-api/) — The Leads API from Alto (Vebra / Zoopla) — 2 operation(s) for leads.
- [Alto (Vebra / Zoopla) Lettings Progression API](https://apis.io/apis/alto-vebra/alto-vebra-lettingsprogression-api/) — The LettingsProgression API from Alto (Vebra / Zoopla) — 1 operation(s) for lettingsprogression.
- [Alto (Vebra / Zoopla) Listing API](https://apis.io/apis/alto-vebra/alto-vebra-listing-api/) — The Listing API from Alto (Vebra / Zoopla) — 7 operation(s) for listing.
- [Alto (Vebra / Zoopla) Management Events API](https://apis.io/apis/alto-vebra/alto-vebra-managementevents-api/) — The ManagementEvents API from Alto (Vebra / Zoopla) — 3 operation(s) for managementevents.
- [Alto (Vebra / Zoopla) Media API](https://apis.io/apis/alto-vebra/alto-vebra-media-api/) — The Media API from Alto (Vebra / Zoopla) — 3 operation(s) for media.
- [Alto (Vebra / Zoopla) Negotiators API](https://apis.io/apis/alto-vebra/alto-vebra-negotiators-api/) — The Negotiators API from Alto (Vebra / Zoopla) — 2 operation(s) for negotiators.
- [Alto (Vebra / Zoopla) Offers API](https://apis.io/apis/alto-vebra/alto-vebra-offers-api/) — The Offers API from Alto (Vebra / Zoopla) — 1 operation(s) for offers.
- [Alto (Vebra / Zoopla) Owners API](https://apis.io/apis/alto-vebra/alto-vebra-owners-api/) — The Owners API from Alto (Vebra / Zoopla) — 1 operation(s) for owners.
- [Alto (Vebra / Zoopla) Parameters API](https://apis.io/apis/alto-vebra/alto-vebra-parameters-api/) — The Parameters API from Alto (Vebra / Zoopla) — 6 operation(s) for parameters.
- [Alto (Vebra / Zoopla) Partners API](https://apis.io/apis/alto-vebra/alto-vebra-partners-api/) — The Partners API from Alto (Vebra / Zoopla) — 3 operation(s) for partners.
- [Alto (Vebra / Zoopla) Products API](https://apis.io/apis/alto-vebra/alto-vebra-products-api/) — The Products API from Alto (Vebra / Zoopla) — 4 operation(s) for products.
- [Alto (Vebra / Zoopla) Reference Checks API](https://apis.io/apis/alto-vebra/alto-vebra-referencechecks-api/) — The ReferenceChecks API from Alto (Vebra / Zoopla) — 2 operation(s) for referencechecks.
- [Alto (Vebra / Zoopla) Referral API](https://apis.io/apis/alto-vebra/alto-vebra-referral-api/) — The Referral API from Alto (Vebra / Zoopla) — 1 operation(s) for referral.
- [Alto (Vebra / Zoopla) Referrals API](https://apis.io/apis/alto-vebra/alto-vebra-referrals-api/) — The Referrals API from Alto (Vebra / Zoopla) — 1 operation(s) for referrals.
- [Alto (Vebra / Zoopla) REST Endpoints API](https://apis.io/apis/alto-vebra/alto-vebra-rest-endpoints-api/) — The REST Endpoints API from Alto (Vebra / Zoopla) — 2 operation(s) for rest endpoints.
- [Alto (Vebra / Zoopla) Sales Progression API](https://apis.io/apis/alto-vebra/alto-vebra-salesprogression-api/) — The SalesProgression API from Alto (Vebra / Zoopla) — 2 operation(s) for salesprogression.
- [Alto (Vebra / Zoopla) Suppliers API](https://apis.io/apis/alto-vebra/alto-vebra-suppliers-api/) — The Suppliers API from Alto (Vebra / Zoopla) — 3 operation(s) for suppliers.
- [Alto (Vebra / Zoopla) Tenancies API](https://apis.io/apis/alto-vebra/alto-vebra-tenancies-api/) — The Tenancies API from Alto (Vebra / Zoopla) — 6 operation(s) for tenancies.
- [Alto (Vebra / Zoopla) File Notes API](https://apis.io/apis/alto-vebra/alto-vebra-file-notes-api/) — The File Notes API from Alto (Vebra / Zoopla) — 4 operation(s) for file notes.
- [Alto (Vebra / Zoopla) Work Orders API](https://apis.io/apis/alto-vebra/alto-vebra-work-orders-api/) — The Work Orders API from Alto (Vebra / Zoopla) — 3 operation(s) for work orders.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (2)

Event-driven and webhook contracts.

- [Alto Webhooks](https://apis.io/asyncapis/alto-vebra/alto-vebra-alto-webhooks-asyncapi/)
- [Zoopla Lead Push Service](https://apis.io/asyncapis/alto-vebra/alto-vebra-zoopla-leads-push-asyncapi/)

#### Event channels (2)

Individual events and webhooks the provider emits.

- [/](https://apis.io/channels/alto-vebra/altonotifications/)
- [/](https://apis.io/channels/alto-vebra/zooplaleads/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [alto-vebra](https://apis.io/servers/alto-vebra/alto-vebra/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Alto Vebra Agentic Access](https://apis.io/agentic-access/alto-vebra/alto-vebra-agentic-access/)

#### Collections (4)

Postman and Open Collection request collections.

- [Alto API](https://apis.io/collections/alto-vebra/open-alto-api/)
- [Leads API](https://apis.io/collections/alto-vebra/open-zoopla-leads-api/)
- [Premium Listing activations](https://apis.io/collections/alto-vebra/open-zoopla-premium-listing-activations/)
- [Weekly Featured Property (WFP) Activations](https://apis.io/collections/alto-vebra/open-zoopla-weekly-featured-property/)

#### Overlays (4)

OpenAPI overlays, including conversational phrasing for each operation.

- [Alto Vebra Alto Api Overlay](https://apis.io/overlays/alto-vebra/alto-vebra-alto-api-overlay/)
- [Alto Vebra Zoopla Leads Api Overlay](https://apis.io/overlays/alto-vebra/alto-vebra-zoopla-leads-api-overlay/)
- [Alto Vebra Zoopla Premium Listing Activations Overlay](https://apis.io/overlays/alto-vebra/alto-vebra-zoopla-premium-listing-activations-overlay/)
- [Alto Vebra Zoopla Weekly Featured Property Overlay](https://apis.io/overlays/alto-vebra/alto-vebra-zoopla-weekly-featured-property-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Alto Vebra Authentication](https://apis.io/security/alto-vebra/alto-vebra-authentication/)
- [Alto Vebra Domain Security](https://apis.io/security/alto-vebra/alto-vebra-domain-security/)
- [Alto Vebra Vulnerability Disclosure](https://apis.io/security/alto-vebra/alto-vebra-vulnerability-disclosure/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Alto Vebra Scopes](https://apis.io/scopes/alto-vebra/alto-vebra-scopes/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.altosoftware.co.uk/)
- [Documentation](https://developers.vebraalto.com/)
- [Getting started](https://developers.vebraalto.com/guides/authenticating-your-requests/)
- [API reference](https://developers.vebraalto.com/api)
- [Sign up](https://www.altosoftware.co.uk/become-a-partner/)
- [Support](https://partnerfeedback.vebraalto.com/)
- [Blog](https://www.altosoftware.co.uk/blog/)
- [Security](https://www.zoopla.co.uk/vulnerability-disclosure/)
- [Terms of service](https://developers.vebraalto.com/api-terms-of-use)
- [Privacy policy](https://www.altosoftware.co.uk/privacy-notice/)
- [GitHub](https://github.com/AltoSoftware)

## API Evangelist rating

**Kin Score 49.5** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 54.2 |
| Contract governance | 4.5 |
| Operational transparency | 36.8 |
| Developer ergonomics | 66.1 |
| Access clarity | 34.2 |

**Agent readiness 41.6** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | — |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | — |
| Event Surface Described | derived (partial credit) |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | — |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 40.2** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/alto-vebra/](https://apis.io/providers/alto-vebra/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Alto (Vebra / Zoopla): the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/alto-vebra/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
