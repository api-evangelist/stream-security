---
name: stream-security-triage-detection
description: >-
  Triage a Stream Security threat detection end to end - list open detections, read the AI summary,
  pull the affected resource and its violations and attack paths, then record a verdict by setting
  the detection status and posting an analyst comment.
api: Stream Security API
base_url: https://{app}.streamsec.io/openapi
operations:
- detections-list
- detections-summary
- inventory-details
- rules-resourceViolations
- attackPaths-details
- detections-setStatus
- detections-comment-create
generated: '2026-08-29'
method: generated
source: >-
  Grounded in openapi/stream-security-api-openapi.json - every operationId above is verified
  present in the spec. Semantics from https://docs.streamsec.io/reference/.
---

# Triage a Stream Security detection

## Before you start

- Authenticate every request with `Authorization: Bearer <API token>`. Tokens are minted in the
  Stream UI under Organization/Workspace Settings → API Token Management and shown only once.
- If your token reaches more than one workspace, send the target workspace ID in the `workspace`
  header on every call. `workspaces-list` (`GET /workspaces`) tells you which ones you can reach.
- Setting a status and posting a comment are **writes**. There is no `Idempotency-Key` on this API,
  so a blind retry of step 6 will post a duplicate comment — see the warning there.

## Steps

1. **List candidate detections.** `GET /detections` (`detections-list`). Filter by `detection_id`,
   `resource_id` or workspace, and page with `skip`/`limit`. Each entry carries severity, account,
   resource details, source, MITRE ATT&CK categories, signal types and any anomalous actions.

2. **Read the platform's own verdict first.** `GET /detections/{detection_id}/ai_summary`
   (`detections-summary`) returns a concise verdict, a confidence score and a contextual
   explanation of the activity, including whether further investigation is recommended. Use it to
   decide whether steps 3–5 are worth the calls.

3. **Identify the asset.** `GET /inventory/resource` (`inventory-details`) for the `resource_id` on
   the detection. This returns type, display name, cloud provider, account, region, public
   accessibility, tags and — for container workloads — cluster/namespace context, container specs,
   environment variables, volume mounts and owner references. `GET /inventory/crown_jewels`
   (`inventory-crownJewels`) tells you whether the resource is business-critical; an empty response
   means none of the resources you asked about are crown jewels.

4. **Pull the posture context.** `GET /rules/resource/{resource_id}/violations`
   (`rules-resourceViolations`) returns every misconfiguration, excessive permission and risky
   exposure on the asset, each with category, severity, rule name, finding type and the timestamp it
   was first detected.

5. **Establish blast radius.** `GET /attack_paths/details/{resource_id}` (`attackPaths-details`)
   returns the ordered path(s) an attacker could traverse to reach the resource, starting from the
   origin (for example, Internet) and listing each gateway, ACL, security group or load balancer in
   between. This is what separates a real exposure from a noisy finding.

6. **Record the verdict.**
   - `PUT /detections/status` (`detections-setStatus`) moves the detection to its investigation
     state — open, in progress or closed. This one is safe to retry: it sets state rather than
     appending, so re-sending the same status is a no-op.
   - `POST /detections/comment` (`detections-comment-create`) attaches your analyst notes.
     **This write is not reversible.** There is no delete-comment or edit-comment operation
     anywhere in the API, and no idempotency key, so a retry after a timeout leaves two comments
     that cannot be removed. Confirm with a `GET /detections` read before re-sending.

## Error handling

All operations return the same five statuses with a `{code, message, issues[]}` JSON body — this
API is **not** RFC 9457, so do not parse for `type`/`title`/`detail`.

| Status | Code | What to do |
| --- | --- | --- |
| 400 | `BAD_REQUEST` | Read `issues[]` for the fields that failed validation. |
| 401 | `UNAUTHORIZED` | Token missing, malformed or expired. Tokens expire on the interval chosen at creation. |
| 403 | `FORBIDDEN` | Authenticated but outside the token's permission level or workspace scope. |
| 404 | `NOT_FOUND` | Wrong identifier, or right identifier in the wrong workspace — check the `workspace` header. |
| 500 | `INTERNAL_SERVER_ERROR` | Retry with backoff. |

No 429 is declared and no rate limits are published, so back off on your own schedule; there is no
`Retry-After` or `RateLimit-*` header to read.
