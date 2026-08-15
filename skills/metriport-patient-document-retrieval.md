---
generated: '2026-08-14'
method: generated
name: Retrieve a patient's clinical documents
description: Register a patient, run a document query across the networks, list the results, and mint a signed download URL for each document.
api: openapi/metriport-document-api-openapi.yml
operations: [createPatient, startDocumentQuery, getDocumentQueryStatus, listDocuments, getDocumentUrl]
source: >-
  Grounded in arazzo/metriport-patient-document-retrieval-workflow.yml; every
  operationId was verified verbatim in openapi/metriport-document-api-openapi.yml
  and openapi/metriport-patient-api-openapi.yml. Lifecycle status of the
  document-query operations is recorded in lifecycle/metriport-lifecycle.yml.
---

# Retrieve a patient's clinical documents

Pull a patient's clinical documents (C-CDA XML, PDFs, images) out of the CommonWell and Carequality networks.

## Status warning
`startDocumentQuery` and `getDocumentQueryStatus` are documented under Metriport's **legacy** API reference and are labelled "(Legacy)" in the published rate-limit table. The current surface is **Network Query**, which fans out to HIE, pharmacy and lab sources and delivers `network-query.*` webhooks. Use this skill against the operations captured in `openapi/`; check `lifecycle/metriport-lifecycle.yml` before building new integrations on it.

## Auth
- `x-api-key: <key>`. Base URL `https://api.metriport.com`. See `authentication/metriport-authentication.yml`.

## Steps
1. **Register the patient** — `createPatient` (`POST /medical/v1/patient?facilityId=...`). Capture the patient `id`.
2. **Start the query** — `startDocumentQuery` (`POST /medical/v1/document/query`) with `patientId` and `facilityId`. The body's `download` and `convert` blocks each report a `Progress` object (`status`, `total`, `successful`, `errors`).
3. **Wait** — the result arrives on your webhook. To poll, call `getDocumentQueryStatus` (`GET /medical/v1/document/query?patientId=...`) and read `download.status` and `convert.status` until neither is `processing`.
4. **List what was retrieved** — `listDocuments` (`GET /medical/v1/document?patientId=...&facilityId=...`). Each `DocumentReference` carries `id`, `fileName`, `description`, `status`, `contentType`, `size` and `indexed`.
5. **Get a download URL** — `getDocumentUrl` (`GET /medical/v1/document/download-url?fileName=...`) returns a short-lived signed URL. Fetch the bytes from that URL directly; do not send `x-api-key` to it.

## Rate limits
- `startDocumentQuery` is capped at **20 requests per minute** (1 every 3 seconds) per account. See `rate-limits/metriport-rate-limits.yml`.

## Pagination
- `listDocuments` is a paginated list: `count` (default 50, max 500), `fromItem`, `toItem`; follow `meta.nextPage` until it is absent. Only two of the three parameters may be sent at once. See `conventions/metriport-conventions.yml`.

## Retries
- No `Idempotency-Key` exists. Poll status before restarting a query rather than resubmitting step 2.

## Errors
- `{"status","name","title","detail"}` in `application/json`. See `errors/metriport-problem-types.yml`.

## Testing
- Sandbox patients matched by first name return roughly six documents each: a C-CDA XML plus the resulting FHIR resources, three PDFs and two images. See `sandbox/metriport-sandbox.yml`.
