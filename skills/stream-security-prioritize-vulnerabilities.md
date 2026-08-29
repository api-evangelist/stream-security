---
name: stream-security-prioritize-vulnerabilities
description: >-
  Prioritise CVE remediation by exposure rather than raw CVSS - list vulnerabilities filtered by
  exploitability, fix availability and internet exposure, expand each to the affected resources, and
  confirm blast radius before raising the work.
api: Stream Security API
base_url: https://{app}.streamsec.io/openapi
operations:
- cve-listCves
- cve-getCve
- cve-listCveResources
- inventory-crownJewels
- attackPaths-details
- inventory-details
generated: '2026-08-29'
method: generated
source: >-
  Grounded in openapi/stream-security-api-openapi.json - every operationId above is verified
  present in the spec. Semantics from https://docs.streamsec.io/reference/.
---

# Prioritise vulnerabilities by real exposure

The point of this flow is to stop ranking by CVSS alone. Stream Security carries exploit
availability, fix availability and internet exposure as filter dimensions, so you can sort the
backlog by what an attacker can actually reach.

## Before you start

- `Authorization: Bearer <API token>` on every request; add the `workspace` header if your token
  spans workspaces.
- Every operation in this flow is a **read**. Nothing here mutates state, so retries are safe.

## Steps

1. **Filter the backlog down to what matters.** `GET /cve` (`cve-listCves`) supports filtering by
   `cve_id`, account, resource, resource type, package name, severity, exploit availability, fix
   availability, internet exposure and region. Start with the intersection that actually creates
   risk: exploit available **and** fix available **and** internet exposed. Sort by `cvss_score`,
   severity, discovery time or published date; page with `skip`/`limit`.

2. **Read the detail on the survivors.** `GET /cve/{cve_id}` (`cve-getCve`) returns the full record
   — severity, `cvss_score`, `cvss_scoring_vector`, `cvss_version`, exploit and fix availability,
   affected packages and remediation guidance.

3. **Expand to affected resources.** `GET /cve/resources` (`cve-listCveResources`) takes `cve_ids`
   as a comma-separated CVE list (for example `cve_ids=CVE-2021-44228,CVE-2021-45046`) and returns
   the resources carrying them, with pagination. For filters too complex for a query string — tag
   matching in particular — the documentation directs you to the `POST /cve/resources/query`
   variant instead.

4. **Check business criticality.** `GET /inventory/crown_jewels` (`inventory-crownJewels`) with the
   affected resource IDs. An empty response means none of them are marked crown jewels. Anything
   that comes back should jump the queue.

5. **Confirm reachability.** `GET /attack_paths/details/{resource_id}` (`attackPaths-details`) for
   each high-value affected resource. A CVE on a resource with no path from the Internet is a
   different ticket than the same CVE on one with a clear traversal, and this is where you prove
   which you are looking at.

6. **Fill in the deployment context.** `GET /inventory/resource` (`inventory-details`) returns
   container specs, image references, cluster and namespace context — what the remediation owner
   needs in order to actually patch.

## Notes

- `cve_id`, `cvss_score`, `cvss_scoring_vector` and `cvss_version` are structured fields, not free
  text, so you can filter and sort on them without a bespoke mapping layer.
- Array filters accept comma-separated values.
- Errors follow the shared `{code, message, issues[]}` envelope — see
  `errors/stream-security-problem-types.yml`. This API is not RFC 9457.
