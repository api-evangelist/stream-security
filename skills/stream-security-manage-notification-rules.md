---
name: stream-security-manage-notification-rules
description: >-
  Create, inspect, amend and safely retire Stream Security notification rules - the mechanism that
  routes cloud events, detections and simulation events to webhooks, Slack, PagerDuty, Splunk, Teams,
  Opsgenie, Logz.io, Google Chat, Cortex XSIAM and Torq.
api: Stream Security API
base_url: https://{app}.streamsec.io/openapi
operations:
- notifications-list
- notifications-get
- notifications-create
- notifications-update
- notifications-delete
generated: '2026-08-29'
method: generated
source: >-
  Grounded in openapi/stream-security-api-openapi.json - every operationId above is verified
  present in the spec, and the enum values below are read from the POST /notifications request body
  schema. Semantics from https://docs.streamsec.io/reference/.
---

# Manage notification rules

Notification rules are the **only fully CRUD-able entity** in the Stream Security API, and they are
where its whole event surface lives — there is no separate webhook subscription endpoint. A rule
binds an event type to one or more destination channels through a filter condition tree.

## Before you start

- `Authorization: Bearer <API token>`, plus the `workspace` header when your token spans workspaces.
- Your token needs **Read & Write** permission. A read-only token will get `403 FORBIDDEN`.
- **This flow contains the most dangerous operation in the API.** Read the reversibility section
  before you call `DELETE`.

## Steps

1. **See what already exists.** `GET /notifications` (`notifications-list`) returns rules in
   descending creation order, with filtering and pagination. Do this first — creating a duplicate
   rule doubles alert volume, and there is no idempotency key to protect you.

2. **Read one in full.** `GET /notifications/{id}` (`notifications-get`) returns the complete
   configuration: channels, conditions and settings.

3. **Create a rule.** `POST /notifications` (`notifications-create`). The body requires `name`
   (1–100 chars) and `event_type`, and accepts `description` (max 250 chars), `enabled` (default
   `true`), `channels[]` and `condition`.

   - `event_type` is one of: `cloud_event`, `detection`, `simulation_event`.
   - Each channel is `{type, subtype, id}` where type is one of: `webhook`, `slack`, `splunk`,
     `pagerduty`, `microsoftteams`, `opsgenie`, `logzio`, `googlecards`, `paloaltocortexxsiam`,
     `torq`. `webhook` is the generic HTTP-callback path.
   - `condition.main_filter` is a nested boolean tree: an `operand` (`and`/`or`) over `filters[]`,
     where each filter is a `field`, a `match_type` (`is`, `is_not`, `contains`, `not_contains`,
     `regex`, `gte`, `lte`, `exists`, `not_exists`, `empty`, `not_empty`) and a `value`. Filters can
     nest further filter groups, and tags match through their own `{key, match_type, value}`
     structure.

   Start `enabled: false`, verify the rule reads back the way you intended, then enable it.

4. **Amend a rule.** `PATCH /notifications/{id}` (`notifications-update`) supports partial updates —
   only the fields you send are modified.

   > **Read before you write.** There is no version history, no revision endpoint and no undo
   > operation on this resource. If you want to be able to put a rule back the way it was, call
   > `GET /notifications/{id}` and keep the response *before* you PATCH. Nothing else will recover it.

5. **Retire a rule — prefer disabling.** `PATCH /notifications/{id}` with `enabled: false` stops the
   rule firing while keeping its configuration intact, and is fully reversible by setting
   `enabled: true` again. **Use this instead of deletion wherever you can.**

6. **Delete only when you mean it.** `DELETE /notifications/{id}` (`notifications-delete`). The
   provider's own description is unambiguous: *"Permanently deletes a notification rule. This action
   cannot be undone."* There is no restore endpoint, no soft delete and no retention window. An
   agent should never call this without explicit human confirmation.

## Reversibility summary

| Operation | Reversible | How | Window |
| --- | --- | --- | --- |
| `POST /notifications` | Yes | `DELETE /notifications/{id}`, or PATCH `enabled:false` | none stated |
| `PATCH /notifications/{id}` | Only with a prior read | PATCH the captured prior state back | none stated |
| `DELETE /notifications/{id}` | **No** | — | — |

## Delivery caveats

Stream.Security publishes no payload signing scheme, no retry/backoff policy and no replay
protection for webhook delivery, and does not publish the payload shape for any of the three event
types. A receiver cannot cryptographically verify that a delivered payload came from Stream
Security. See `asyncapi/stream-security-notifications-webhooks.yml`.
