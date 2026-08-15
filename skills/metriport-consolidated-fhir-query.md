---
generated: '2026-08-14'
method: generated
name: Query a patient's consolidated FHIR data
description: Register a patient, start a consolidated FHIR R4 query for the resources you need, wait for the webhook, then count what came back.
api: openapi/metriport-consolidated-api-openapi.yml
operations: [createPatient, startConsolidatedQuery, getConsolidatedQueryStatus, countConsolidatedData]
source: >-
  Grounded in arazzo/metriport-consolidated-fhir-query-workflow.yml; every
  operationId was verified verbatim in openapi/metriport-patient-api-openapi.yml
  and openapi/metriport-consolidated-api-openapi.yml. Cross-cutting rules cite
  conventions/metriport-conventions.yml, errors/metriport-problem-types.yml,
  asyncapi/metriport-webhooks.yml and sandbox/metriport-sandbox.yml.
---

# Query a patient's consolidated FHIR data

Get a deduplicated FHIR R4 bundle for one patient out of Metriport's Medical API.

## Auth
- `x-api-key: <key>` on every request. One static key, full account access, no scopes. See `authentication/metriport-authentication.yml`.
- Base URL `https://api.metriport.com`; sandbox `https://api.sandbox.metriport.com`. Keys are not interchangeable between them.

## Before you start
- Configure a webhook URL first (`updateSettings`). This flow is asynchronous — the data arrives as a `medical.consolidated-data` webhook, not in the response. See `asyncapi/metriport-webhooks.yml`.
- You need a `facilityId`. Create one with `createFacility` if you have none.

## Steps
1. **Register the patient** — `createPatient` (`POST /medical/v1/patient?facilityId=...`). Body carries `firstName`, `lastName`, `dob`, `genderAtBirth`, `address[]`, optional `contact[]` and `externalId`. Capture the returned patient `id`.
2. **Start the query** — `startConsolidatedQuery` (`POST /medical/v1/patient/{id}/consolidated/query`). Pass the `resources` you want (FHIR R4 resource type names), an optional `dateFrom`/`dateTo`, and `conversionType` if you want a rendered document rather than raw FHIR. Capture `requestId`.
3. **Wait** — the result is delivered to your webhook as `medical.consolidated-data` carrying the same `requestId`. If you must poll instead, call `getConsolidatedQueryStatus` (`GET /medical/v1/patient/{id}/consolidated/query`) and read `status` until it leaves `processing`.
4. **Count what you got** — `countConsolidatedData` (`GET /medical/v1/patient/{id}/consolidated/count`) returns per-resource-type counts, which is the cheap way to confirm the bundle is non-empty before you download it.

## Rate limits
- `startConsolidatedQuery` is capped at **120 requests per minute** (2/second) per account. No rate-limit response headers exist, so pace to the number rather than waiting for a signal. See `rate-limits/metriport-rate-limits.yml`.

## Retries
- **Do not blind-retry step 2.** Metriport publishes no `Idempotency-Key` and no replay semantics, so a retried start can begin a second query. Poll `getConsolidatedQueryStatus` before resubmitting. See `conventions/metriport-conventions.yml`.

## Errors
- Failures come back as `{"status","name","title","detail"}` in `application/json` — not `application/problem+json`. A missing patient or facility surfaces as `status: 404`, `name: NOT_FOUND`. See `errors/metriport-problem-types.yml`.

## Testing
- In sandbox, create the patient with a first name of `Jane`, `Chris`, `Ollie`, `Andreas` or `Kyla` to get that persona's example clinical data. Any other first name returns a pre-defined file when `conversionType` is set. See `sandbox/metriport-sandbox.yml`.
