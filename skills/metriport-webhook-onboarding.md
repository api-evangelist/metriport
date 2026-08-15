---
generated: '2026-08-14'
method: generated
name: Wire up and verify Metriport webhooks
description: Register a webhook URL over the API, answer the ping handshake, verify the HMAC signature, and replay failed deliveries.
api: openapi/metriport-settings-api-openapi.yml
operations: [updateSettings, getSettings, getWebhookStatus, retryWebhookRequests]
source: >-
  operationIds verified verbatim in openapi/metriport-settings-api-openapi.yml;
  behaviour read from
  https://docs.metriport.com/medical-api/getting-started/webhooks and captured in
  asyncapi/metriport-webhooks.yml.
---

# Wire up and verify Metriport webhooks

Every long-running Metriport operation — network queries, consolidated data queries, bulk patient create, bulk document download, message delivery, patient ADT notifications — returns its result on a webhook. Nothing else works until this is done.

## Auth
- `x-api-key: <key>`. See `authentication/metriport-authentication.yml`.

## Endpoint requirements
Your endpoint must:
- be publicly reachable over HTTPS and **not** redirect (Metriport does not follow redirects);
- accept `POST` and respond `200` in **under 4 seconds** — process asynchronously;
- answer the `ping` handshake;
- verify `x-metriport-signature`;
- be idempotent — the same payload may arrive more than once.

## Steps
1. **Register the URL** — `updateSettings` (`POST /settings`) with your `webhookUrl`. This generates the account's webhook key. Metriport immediately sends a `ping`.
2. **Read back the key** — `getSettings` (`GET /settings`) returns `webhookUrl`, `webhookKey` and `webhookEnabled`. Store `webhookKey` as a secret.
3. **Answer the ping** — on a body of `{"ping": "<random-sequence>", "meta": {..., "type": "ping"}}`, respond `200` with `{"pong": "<random-sequence>"}`.
4. **Verify every message** — compute `HMAC-SHA256(webhookKey, rawBody)` and compare it constant-time against the `x-metriport-signature` header. Compute it over the **raw** body; parsing first can change the bytes enough to invalidate the signature. Discard on mismatch.
5. **Check for failures** — `getWebhookStatus` (`GET /settings/webhook`) reports how many deliveries are processing and how many failed.
6. **Replay** — `retryWebhookRequests` (`POST /settings/webhook/retry`) re-sends the failed ones. Metriport performs **no automatic retries**, so this step is not optional if step 5 shows failures.

## Rotating the webhook key
Set `webhookUrl` to an empty string with `updateSettings`, then set it again. There is no dedicated rotate operation.

## Events to handle
Sixteen types across five prefixes — `network-query.*`, `medical.*`, `message.*`, `patient.*`, `ias.*`, plus `ping`. Switch on `meta.type`. Full catalogue in `asyncapi/metriport-webhooks.yml`.

## Correlation
`meta.messageId` identifies the delivery; `meta.requestId` ties it back to the API call that started the flow; `meta.data` echoes whatever metadata you passed on that call (absent on real-time patient notifications).

## Testing
In sandbox, the dashboard's "Test events" control sends Patient Admit / Transfer / Discharge payloads to your endpoint. See `sandbox/metriport-sandbox.yml`.

## Errors
`{"status","name","title","detail"}` in `application/json`. See `errors/metriport-problem-types.yml`.
