# Luminance

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

Luminance Technologies Ltd. is a UK-headquartered legal-AI company, founded in 2015 out of Cambridge mathematics research, that builds what it markets as Legal-Grade AI for the full contract lifecycle — drafting, negotiation, analysis, compliance, investigation and collaboration. The platform is delivered as a per-customer instance (an "instance moniker" subdomain) and exposes a documented RESTful HTTP/JSON API that lets external software read and act on projects, folders, documents, matters, matter versions, tasks, reviews, annotations, workflows and document templates, plus machine-learning surfaces such as Traffic Light Analysis and annotation-driven contract intelligence. Three OpenAPI 3.0 versions are published from Luminance's own API host: v1.3.0 and v1.4.0 (OAuth2 client-credentials) and the newer "Public API v2" v1.5, which is deployed by standard to Luminance product versions 1.43.0 onward. Authentication is OAuth2 client credentials against the customer instance token endpoint, and API traffic is rate limited to 100 requests every 10 minutes.

**Areas:** Company · Legal · Artificial Intelligence · Contracts · Contract Lifecycle Management · Document Intelligence · Compliance · Legal Tech · Enterprise Software · Automation

## Luminance on APIs.io

Everything profiled for Luminance is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/luminance/](https://apis.io/providers/luminance/)** — or go straight to one of the APIs or properties below.

### APIs (21)

- [Luminance Accounts API](https://apis.io/apis/luminance/luminance-accounts-api/) — The Accounts API from Luminance — 6 operation(s) for accounts.
- [Luminance Annotation Source Relations API](https://apis.io/apis/luminance/luminance-annotation-source-relations-api/) — The Annotation Source Relations API from Luminance — 2 operation(s) for annotation source relations.
- [Luminance Annotation Sources API](https://apis.io/apis/luminance/luminance-annotation-sources-api/) — The Annotation Sources API from Luminance — 2 operation(s) for annotation sources.
- [Luminance Annotation Types API](https://apis.io/apis/luminance/luminance-annotation-types-api/) — The Annotation Types API from Luminance — 2 operation(s) for annotation types.
- [Luminance Annotations API](https://apis.io/apis/luminance/luminance-annotations-api/) — The Annotations API from Luminance — 12 operation(s) for annotations.
- [Luminance Contract Creation API](https://apis.io/apis/luminance/luminance-contract-creation-api/) — The Contract Creation API from Luminance — 4 operation(s) for contract creation.
- [Luminance Document Templates API](https://apis.io/apis/luminance/luminance-document-templates-api/) — The Document Templates API from Luminance — 4 operation(s) for document templates.
- [Luminance Documents API](https://apis.io/apis/luminance/luminance-documents-api/) — The Documents API from Luminance — 19 operation(s) for documents.
- [Luminance Folders API](https://apis.io/apis/luminance/luminance-folders-api/) — The Folders API from Luminance — 10 operation(s) for folders.
- [Luminance Matter Versions API](https://apis.io/apis/luminance/luminance-matter-versions-api/) — The Matter Versions API from Luminance — 4 operation(s) for matter versions.
- [Luminance Matters API](https://apis.io/apis/luminance/luminance-matters-api/) — The Matters API from Luminance — 22 operation(s) for matters.
- [Luminance Project Users API](https://apis.io/apis/luminance/luminance-project-users-api/) — The Project Users API from Luminance — 2 operation(s) for project users.
- [Luminance Projects API](https://apis.io/apis/luminance/luminance-projects-api/) — The Projects API from Luminance — 6 operation(s) for projects.
- [Luminance Reviews API](https://apis.io/apis/luminance/luminance-reviews-api/) — The Reviews API from Luminance — 3 operation(s) for reviews.
- [Luminance Root API](https://apis.io/apis/luminance/luminance-root-api/) — The Root API from Luminance — 1 operation(s) for root.
- [Luminance Search API](https://apis.io/apis/luminance/luminance-search-api/) — The Search API from Luminance — 3 operation(s) for search.
- [Luminance System API](https://apis.io/apis/luminance/luminance-system-api/) — The System API from Luminance — 1 operation(s) for system.
- [Luminance Tasks API](https://apis.io/apis/luminance/luminance-tasks-api/) — The Tasks API from Luminance — 14 operation(s) for tasks.
- [Luminance Traffic Light Analysis API](https://apis.io/apis/luminance/luminance-traffic-light-analysis-api/) — The Traffic Light Analysis API from Luminance — 3 operation(s) for traffic light analysis.
- [Luminance Users API](https://apis.io/apis/luminance/luminance-users-api/) — The Users API from Luminance — 10 operation(s) for users.
- [Luminance Workflows API](https://apis.io/apis/luminance/luminance-workflows-api/) — The Workflows API from Luminance — 4 operation(s) for workflows.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [luminance](https://apis.io/servers/luminance/luminance/)

#### Collections (20)

Postman and Open Collection request collections.

- [Luminance Accounts API](https://apis.io/collections/luminance/open-luminance-accounts-api/)
- [Luminance Public API v2 Annotation Source Relations API](https://apis.io/collections/luminance/open-luminance-annotation-source-relations-api/)
- [Luminance Public API v2 Annotation Sources API](https://apis.io/collections/luminance/open-luminance-annotation-sources-api/)
- [Luminance Public API v2 Annotation Types API](https://apis.io/collections/luminance/open-luminance-annotation-types-api/)
- [Luminance Annotations API](https://apis.io/collections/luminance/open-luminance-annotations-api/)
- [Luminance Contract Creation API](https://apis.io/collections/luminance/open-luminance-contract-creation-api/)
- [Luminance Public API v2 Document Templates API](https://apis.io/collections/luminance/open-luminance-document-templates-api/)
- [Luminance Documents API](https://apis.io/collections/luminance/open-luminance-documents-api/)
- [Luminance Folders API](https://apis.io/collections/luminance/open-luminance-folders-api/)
- [Luminance Matter Versions API](https://apis.io/collections/luminance/open-luminance-matter-versions-api/)
- [Luminance Matters API](https://apis.io/collections/luminance/open-luminance-matters-api/)
- [Luminance Public API v2 Project Users API](https://apis.io/collections/luminance/open-luminance-project-users-api/)
- [Luminance Projects API](https://apis.io/collections/luminance/open-luminance-projects-api/)
- [Luminance Root API](https://apis.io/collections/luminance/open-luminance-root-api/)
- [Luminance Public API v2 Search API](https://apis.io/collections/luminance/open-luminance-search-api/)
- [Luminance Public API v2 System API](https://apis.io/collections/luminance/open-luminance-system-api/)
- [Luminance Tasks API](https://apis.io/collections/luminance/open-luminance-tasks-api/)
- [Luminance Traffic Light Analysis API](https://apis.io/collections/luminance/open-luminance-traffic-light-analysis-api/)
- [Luminance Users API](https://apis.io/collections/luminance/open-luminance-users-api/)
- [Luminance Workflows API](https://apis.io/collections/luminance/open-luminance-workflows-api/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Luminance Public Api V2 Overlay](https://apis.io/overlays/luminance/luminance-public-api-v2-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Luminance Authentication](https://apis.io/security/luminance/luminance-authentication/)
- [Luminance Domain Security](https://apis.io/security/luminance/luminance-domain-security/)
- [Luminance Trust Center](https://apis.io/security/luminance/luminance-trust-center/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Luminance Scopes](https://apis.io/scopes/luminance/luminance-scopes/)

#### Rate limits (1)

Published request limits.

- [Luminance Rate Limits](https://apis.io/rate-limits/luminance/luminance-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.luminance.com/)
- [Documentation](https://api.luminance.com/swagger-docs)
- [API reference](https://api.luminance.com/swagger-docsv150)
- [Sign up](https://www.luminance.com/demo/)
- [Support](https://help.luminance.com/en/)
- [Blog](https://www.luminance.com/resources/blog/)
- [Compliance](https://www.luminance.com/security/)
- [Terms of service](https://www.luminance.com/terms-conditions/)
- [Privacy policy](https://www.luminance.com/privacy-policy/)

## API Evangelist rating

**Kin Score 45.1** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 78.6 |
| Contract quality | 41.8 |
| Contract governance | 18.2 |
| Operational transparency | 21.1 |
| Developer ergonomics | 47.0 |
| Access clarity | 50.0 |

**Agent readiness 26.0** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | negotiable (partial credit) |
| Idempotency | — |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | — |

**Regulatory alignment 36.4** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/luminance/](https://apis.io/providers/luminance/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Luminance: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/luminance/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
