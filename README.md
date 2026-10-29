# Co-Legal

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

Co-Legal B.V. is a Dutch company (KvK 42135345, Delft) building AI-native legal software and dossier support for Belgian and cross-border Belgium–Netherlands matters — wealth planning and succession, company law and transactions, tax and finance, real estate — sold to law firms, notaries, accountants and tax advisers by proposal, with the private platform behind Cloudflare Access and Microsoft Entra. Alongside it Co-Legal runs a public, free, anonymous, read-only agent at agent.co-legal.be for informational Belgian and Dutch legal and fiscal source questions: an A2A 1.0 agent card signed with JWS ES256 (verifiable against a published JWKS) declaring 17 skills — KBO/BCE company lookup, EU VIES VAT validation, Belgian and Dutch ECLI case-law resolvers, EUR-Lex/CELEX and Justel/wetten.overheid.nl statute resolvers, Flemish inheritance-tax brackets, ECB reference rates, IBAN validation, public legal-corpus search and read, a citation verifier, DOCX concept drafting and a natural-language answer skill — and a remote MCP server at https://agent.co-legal.be/mcp that answers an anonymous tools/list with 12 of those as read-only, idempotent tools. Everything runs on Google Cloud in the EU with the model (claude-opus-5 via Vertex AI) disclosed inside the card. No OpenAPI is published; the MCP tools/list and the card's tool-schema extension are the machine-readable contract.

**Areas:** Legal · Legal Research · Tax · Case Law · Legislation · Company Registry · VAT Validation · Belgium · Netherlands · European Union · A2A · MCP

## Co-Legal on APIs.io

Everything profiled for Co-Legal is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/co-legal-be/](https://apis.io/providers/co-legal-be/)** — or go straight to one of the APIs or properties below.

### APIs (2)

- [Co-Legal Public Assistant (A2A Agent)](https://apis.io/apis/co-legal-be/co-legal-public-assistant-a2a-agent/) — Agent2Agent 1.0 surface of Co-Legal's public legal/fiscal assistant. The agent card at https://agent.co-legal.be/.well-known/agent-card.json (version…
- [Co-Legal Legal Lookup MCP Server](https://apis.io/apis/co-legal-be/co-legal-legal-lookup-mcp-server/) — Remote Model Context Protocol server at https://agent.co-legal.be/mcp (Streamable HTTP, POST only, negotiated protocol version 2025-06-18, serverInfo…

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (2)

Model Context Protocol servers that expose the API to agents.

- [co-legal-be-mcp.yml](https://apis.io/servers/co-legal-be/co-legal-be-mcp-yml/)
- [MCP discovery pointer](https://apis.io/servers/co-legal-be/mcp-discovery-pointer/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Co Legal Be Authentication](https://apis.io/security/co-legal-be/co-legal-be-authentication/)
- [Co Legal Be Domain Security](https://apis.io/security/co-legal-be/co-legal-be-domain-security/)
- [Co Legal Be Vulnerability Disclosure](https://apis.io/security/co-legal-be/co-legal-be-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Co Legal Be Plans Pricing](https://apis.io/plans/co-legal-be/co-legal-be-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Co Legal Be Rate Limits](https://apis.io/rate-limits/co-legal-be/co-legal-be-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://co-legal.be/)
- [Documentation](https://co-legal.be/agent)
- [Getting started](https://agent.co-legal.be/)
- [API reference](https://agent.co-legal.be/.well-known/agent-card.json)
- [Pricing](https://agent.co-legal.be/.well-known/payment-options.json)
- [Support](https://co-legal.be/contact)
- [Blog](https://co-legal.be/blog)
- [Security](https://co-legal.be/security)
- [Terms of service](https://co-legal.be/legal)
- [Privacy policy](https://co-legal.be/legal)

## API Evangelist rating

**Kin Score 42.4** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 0.0 |
| Contract governance | 18.2 |
| Operational transparency | 31.6 |
| Developer ergonomics | 58.9 |
| Access clarity | 52.6 |

**Agent readiness 18.0** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | — |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | documented (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | conformant |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | na |

**Regulatory alignment 57.3** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/co-legal-be/](https://apis.io/providers/co-legal-be/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Co-Legal: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/co-legal-be/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
