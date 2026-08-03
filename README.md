# Alto (Vebra / Zoopla) (alto-vebra)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Alto — formerly Vebra Alto, and still trading through vebra.com — is the United Kingdom's most widely deployed estate agency CRM, used by more than 6,000 sales and lettings agencies to run valuations, listings, applicant matching, offers, sales and lettings progression, tenancies, property management, work orders and client accounting. It is owned by Houseful Limited, the parent of the Zoopla portal, which places Alto at the exact chokepoint of the UK residential market — the country has no MLS, so listings reach Rightmove and Zoopla through agency CRM software rather than a shared cooperative database, and Alto is the largest of those pipes. Its API posture is genuinely strong on the contract side and closed on the access side: Alto publishes an open, unauthenticated developer portal at developers.vebraalto.com carrying a complete OpenAPI 3.0.4 document (95 paths across 27 resource families) served verbatim from api-docs.vebraalto.com, alongside 24 documented CloudEvents 1.0 webhook event types. But credentials are partner-only — a developer must register an integration in Alto Connect, be bound by an existing contract with Vebra Solutions, and then wait for an individual agency to activate the integration and issue an AgencyRef before a single call can be made.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/alto-vebra/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/alto-vebra/refs/heads/main/apis.yml)

## Tags

- Real Estate
- United Kingdom
- PropTech
- Property Listings
- CRM
- Property Management
- Rentals
- Conveyancing
- Estate Agency
- Tenancy

## Timestamps

- **Created:** 2026-07-26
- **Modified:** 2026-07-26

## APIs

### Alto API

The full Alto REST API for UK estate agency operations — 95 documented paths across 27 resource families covering contacts and applicants, property inventory, listings and media, appraisals and valuations, appointments and viewings, leads, offers, sales progression, lettings progression, tenancies, landlords and owners, work orders, suppliers, documents, file notes, branches, negotiators and partner integration status. OpenAPI 3.0.4 with a sandbox and a production server, Bearer JWT obtained via OAuth2 client-credentials against the /token endpoint, an AgencyRef header scoping every call to one agency, and route-level scopes of the form `alto/read:contacts` and `alto/route:get-inventory`.

- **Human URL:** [https://developers.vebraalto.com/api](https://developers.vebraalto.com/api)
- **Base URL:** `https://api.alto.zoopla.co.uk`

#### Tags

- Real Estate
- CRM
- Property Listings
- Tenancy
- Property Management
- United Kingdom

#### Properties

- [OpenAPI](openapi/alto-api-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://developers.vebraalto.com/)
- [API Reference](https://developers.vebraalto.com/api)
- [Authentication](https://developers.vebraalto.com/guides/authenticating-your-requests/)
- [Webhooks](https://developers.vebraalto.com/guides/webhooks/)
- [Terms of Service](https://developers.vebraalto.com/api-terms-of-use)
- [Errors](https://developers.vebraalto.com/guides/error-codes/)
- [Glossary](https://developers.vebraalto.com/guides/glossary/)
- [Sandbox](https://developers.vebraalto.com/guides/access-to-sandbox-alto-ui/)
- [Portal](https://connect.vebraalto.com/connect)
- [Support](https://partnerfeedback.vebraalto.com/)

### Zoopla Leads API

Swagger 2.0 poll API for retrieving applicant leads and appraisal (valuation) leads generated on the Zoopla portal, published by Houseful for contracted Zoopla agency customers and their software partners. OAuth2 client-credentials against services-auth.services.zoopla.co.uk with the scopes `leads/list:applicant-leads` and `leads/list:appraisal-leads`. A push variant is documented alongside the poll contract.

- **Human URL:** [https://developers.zoopla.co.uk/leads/reference/api](https://developers.zoopla.co.uk/leads/reference/api)
- **Base URL:** `https://services.zoopla.co.uk`

#### Tags

- Real Estate
- Leads
- Property Listings
- United Kingdom

#### Properties

- [OpenAPI](openapi/zoopla-leads-api-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://developers.zoopla.co.uk/leads/docs/available-lead-services)
- [API Reference](https://developers.zoopla.co.uk/leads/reference/api)
- [Documentation](https://developers.zoopla.co.uk/leads/docs/push-service)
- [Documentation](https://developers.zoopla.co.uk/leads/docs/field-definitions)
- [Authentication](https://developers.zoopla.co.uk/docs/authentication)
- [Terms of Service](https://developers.zoopla.co.uk/docs/terms-of-use)

### Zoopla Premium Listing Activations API

OpenAPI 3.0.0 contract for activating and inspecting Zoopla Premium Listing products against a property listing, exposed at `/products/premium-listings` and `/products/premium-listings/{uuid}`. OAuth2 client-credentials with the `api/api_access` scope.

- **Human URL:** [https://developers.zoopla.co.uk/premium-listings/reference/api](https://developers.zoopla.co.uk/premium-listings/reference/api)
- **Base URL:** `https://services.zoopla.co.uk`

#### Tags

- Real Estate
- Property Listings
- Advertising
- United Kingdom

#### Properties

- [OpenAPI](openapi/zoopla-premium-listing-activations-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://developers.zoopla.co.uk/docs/premium-listings)
- [API Reference](https://developers.zoopla.co.uk/premium-listings/reference/api)
- [Errors](https://developers.zoopla.co.uk/docs/premium-listings-error-codes-register)
- [Authentication](https://developers.zoopla.co.uk/docs/authentication)

### Zoopla Weekly Featured Property (WFP) Activations API

OpenAPI 3.0.0 contract for activating Zoopla Weekly Featured Property placements against a listing, exposed at `/products/weekly-featured-properties` and `/products/weekly-featured-properties/{uuid}`. OAuth2 client-credentials with the `api/api_access` scope.

- **Human URL:** [https://developers.zoopla.co.uk/wfp/reference/api](https://developers.zoopla.co.uk/wfp/reference/api)
- **Base URL:** `https://services.zoopla.co.uk`

#### Tags

- Real Estate
- Property Listings
- Advertising
- United Kingdom

#### Properties

- [OpenAPI](openapi/zoopla-weekly-featured-property-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://developers.zoopla.co.uk/docs/weekly-featured-properties)
- [API Reference](https://developers.zoopla.co.uk/wfp/reference/api)
- [Errors](https://developers.zoopla.co.uk/docs/weekly-featured-properties-error-code-register)
- [Authentication](https://developers.zoopla.co.uk/docs/authentication)

## Common Properties

- [Website](https://www.altosoftware.co.uk/)
- [Documentation](https://developers.vebraalto.com/)
- [Portal](https://connect.vebraalto.com/connect)
- [Blog](https://www.altosoftware.co.uk/blog/)
- [Blog RSS](https://www.altosoftware.co.uk/feed/)
- [Integrations](https://www.altosoftware.co.uk/integrations/)
- [Terms of Service](https://developers.vebraalto.com/api-terms-of-use)
- [Support](https://partnerfeedback.vebraalto.com/)
- [GitHub Organization](https://github.com/AltoSoftware)
- [GitHub Organization](https://github.com/zoopla-eng)

## RESO Posture

**Not RESO certified.** No RESO reference of any kind — Web API certification, Data Dictionary certification, certification directory listing, OData `$metadata` document, or Universal Property Identifier (UPI) — was found in Alto, Vebra, or Zoopla developer material. RESO is a North American standard driven by NAR and MLS participation, and the United Kingdom has no MLS for a RESO endpoint to sit in front of. The nearest UK analogue is the proprietary Rightmove BLM / Real Time Data Feed and portal-specific feeds, which are bilateral commercial contracts rather than an industry-body-mandated machine-readable standard. Alto keys properties on internal integer identifiers scoped by an `AgencyRef` header, not on a UPI.

## Access Gate

**partner-only.** A developer cannot sign up and call these APIs. The documentation and the specs are genuinely open — the full OpenAPI was downloaded anonymously with no key and no login — but credentials require, in order: an integration registered in Alto Connect (a partner login, not a public signup); an existing contract with Vebra Solutions, which the [API Terms of Use](https://developers.vebraalto.com/api-terms-of-use) make binding by describing the API as "a service that allows Vebra Solutions customers to order additional products and services"; and finally a per-agency activation, after which the partner receives the `AgencyRef` by email that scopes every subsequent call. Zoopla's product APIs follow the same pattern for contracted Zoopla agency customers. **Certification-style openness of the contract does not imply reachability of the data.**

## Open Data

**None.** Alto publishes no open, unlicensed, publicly callable dataset. Listing, contact, tenancy and transaction data behind the Alto API belongs to individual agencies and is contractually licensed. The UK's genuinely open property layer sits entirely in the public sector — HM Land Registry Price Paid Data and ownership datasets under the Open Government Licence, and Ordnance Survey open products for addressing and mapping — and is a separate matter from this organization. Alto sits squarely on the private, closed side of that divide.

## Authentication

OAuth 2.0 client credentials producing a Bearer JWT. Base64-encode `clientId:clientSecret`, POST it as an HTTP Basic `Authorization` header to the token endpoint with `grant_type=client_credentials`, then send `Authorization: Bearer <token>` plus an `AgencyRef: <YOUR_AGENCY_REF>` header on every request. 101 distinct scope strings are embedded in the OpenAPI operation descriptions across two naming generations — semantic (`alto/read:contacts`) and mechanical per-route (`alto/route:get-inventory-inventoryid-tenancies`). No `/.well-known/openid-configuration` is served on either the Alto or the Zoopla auth host.

## Webhooks

24 documented event types delivered as CloudEvents 1.0 JSON, covering contacts, properties, branches, appointments, tenancies, offers, sales progression, leads and integration lifecycle. Subscriptions are **not** self-serve and **not** API-driven — a partner emails Alto support with the integration name, endpoint URL, event types and preferred callback authentication (`x-signature` shared secret, HTTP Basic, or OAuth 2.0 client credentials), and Alto configures it manually.

## Notes

No official SDKs, Postman collections, CLI tools, or MCP server are published. For a CRM with 6,000+ agencies and 40+ named PropTech integrations, that absence is itself a finding: the entire integration story is hand-rolled REST against a well-formed spec. A sandbox exists (`https://api.alto.zoopladev.co.uk`, plus a sandbox Alto UI at `sandbox.altotest.co.uk`) but is granted to onboarded partners only.

See [review.yml](review.yml) for the full probe log, RESO posture, access gate, auth model and harvest provenance.
