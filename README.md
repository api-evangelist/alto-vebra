# Alto (Vebra / Zoopla) (alto-vebra)

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
