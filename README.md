# Stream.Security

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

Stream.Security (formerly Lightlytics) is a cloud detection and response (CDR) and real-time CNAPP vendor that builds a live model of a customer's cloud - its "CloudTwin" - by continuously ingesting configuration state and activity from AWS, Azure, GCP, Kubernetes, ECS and VMware vSphere, then correlating posture drift against runtime behaviour to expose exploitable attack paths, excessive privilege, external exposure and active threats. The platform combines cloud-native log ingestion (CloudTrail, VPC Flow Logs, Route53 DNS, ELB/ALB, WAF, Entra ID audit) with eBPF runtime agents on Kubernetes, ECS and standalone VMs, adds canary/trap decoy resources and auto-remediation, and exposes it all through a public REST API and an MCP server so security teams and agents can query inventory, detections, vulnerabilities, attack paths and posture violations programmatically.

**Areas:** Company · Security · Cloud Security · Cloud Detection and Response · CNAPP · Threat Detection · Vulnerability Management · Kubernetes · Observability · DevSecOps · Artificial Intelligence

## Stream.Security on APIs.io

Everything profiled for Stream.Security is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/stream-security/](https://apis.io/providers/stream-security/)** — or go straight to one of the APIs or properties below.

### APIs (13)

- [Stream Security MCP Server](https://apis.io/apis/stream-security/stream-security-mcp-server/) — Hosted remote MCP server that lets an agent query the Stream Security CloudTwin in natural language - resource metadata, configuration changes,…
- [Stream.Security Attack Paths API](https://apis.io/apis/stream-security/stream-security-attack-paths-api/) — The Attack Paths API from Stream.Security — 3 operation(s) for attack paths.
- [Stream.Security Canaries API](https://apis.io/apis/stream-security/stream-security-canaries-api/) — The Canaries API from Stream.Security — 1 operation(s) for canaries.
- [Stream.Security Config Changes API](https://apis.io/apis/stream-security/stream-security-config-changes-api/) — The Config Changes API from Stream.Security — 2 operation(s) for config changes.
- [Stream.Security Detection Rules API](https://apis.io/apis/stream-security/stream-security-detection-rules-api/) — The Detection Rules API from Stream.Security — 2 operation(s) for detection rules.
- [Stream.Security Integrations API](https://apis.io/apis/stream-security/stream-security-integrations-api/) — The Integrations API from Stream.Security — 2 operation(s) for integrations.
- [Stream.Security Inventory API](https://apis.io/apis/stream-security/stream-security-inventory-api/) — The Inventory API from Stream.Security — 5 operation(s) for inventory.
- [Stream.Security Network & Identity Logs API](https://apis.io/apis/stream-security/stream-security-network-identity-logs-api/) — The Network & Identity Logs API from Stream.Security — 3 operation(s) for network & identity logs.
- [Stream.Security Notifications API](https://apis.io/apis/stream-security/stream-security-notifications-api/) — The Notifications API from Stream.Security — 2 operation(s) for notifications.
- [Stream.Security Posture Security API](https://apis.io/apis/stream-security/stream-security-posture-security-api/) — The Posture Security API from Stream.Security — 3 operation(s) for posture security.
- [Stream.Security Threat Detection API](https://apis.io/apis/stream-security/stream-security-threat-detection-api/) — The Threat Detection API from Stream.Security — 4 operation(s) for threat detection.
- [Stream.Security Vulnerabilities API](https://apis.io/apis/stream-security/stream-security-vulnerabilities-api/) — The Vulnerabilities API from Stream.Security — 3 operation(s) for vulnerabilities.
- [Stream.Security Workspaces API](https://apis.io/apis/stream-security/stream-security-workspaces-api/) — The Workspaces API from Stream.Security — 1 operation(s) for workspaces.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Stream Security Notifications Webhooks](https://apis.io/asyncapis/stream-security/stream-security-notifications-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [Stream Security MCP Server](https://apis.io/servers/stream-security/stream-security-mcp-server/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Stream Security Api Overlay](https://apis.io/overlays/stream-security/stream-security-api-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Stream Security Authentication](https://apis.io/security/stream-security/stream-security-authentication/)
- [Stream Security Domain Security](https://apis.io/security/stream-security/stream-security-domain-security/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Stream Security Plans Pricing](https://apis.io/plans/stream-security/stream-security-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Stream Security Rate Limits](https://apis.io/rate-limits/stream-security/stream-security-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.stream.security/)
- [Documentation](https://docs.streamsec.io/)
- [Getting started](https://docs.streamsec.io/docs/onboarding)
- [API reference](https://docs.streamsec.io/reference)
- [Sign up](https://app.streamsec.io/)
- [Support](https://www.stream.security/contact-us)
- [Blog](https://www.stream.security/blog)
- [Terms of service](https://www.stream.security/terms)
- [Privacy policy](https://www.stream.security/privacy-policy)
- [GitHub](https://github.com/lightlytics)

## API Evangelist rating

**Kin Score 39.6** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 61.2 |
| Contract governance | 4.5 |
| Operational transparency | 10.5 |
| Developer ergonomics | 39.9 |
| Access clarity | 28.9 |

**Agent readiness 36.2** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | verified |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | derived (partial credit) |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | partial |
| Operation Distinctiveness | distinct |

**Regulatory alignment 27.3** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/stream-security/](https://apis.io/providers/stream-security/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Stream.Security: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/stream-security/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
