---
name: Metriport
description: Use when building healthcare applications that need to access, manage, and exchange patient medical data across health information exchanges (HIEs), pharmacies, and laboratories. Reach for this skill when creating patient records, querying consolidated medical data in FHIR format, sending secure messages between providers, managing facilities, or contributing data back to health networks.
metadata:
    mintlify-proj: metriport
    version: "1.0"
---

# Metriport Medical API

## Product summary

Metriport Medical API is a healthcare data integration platform that enables applications to query, consolidate, and exchange patient medical records across health information exchanges (HIEs), pharmacies, and laboratories. Agents use it to create and manage patient and facility records, trigger network queries to retrieve medical data from external sources, access deduplicated and standardized FHIR data, and send secure messages between healthcare providers.

**Key files and endpoints:**
- Base URL: `https://api.metriport.com` (production) or `https://api.sandbox.metriport.com` (sandbox)
- API key header: `x-api-key`
- Primary operations: Patient CRUD, Facility CRUD, Network Query, Consolidated Data Query, Message Delivery, Webhook management
- SDK available for Node.js via `@metriport/api-sdk` npm package
- Full API reference: https://docs.metriport.com/medical-api/api-reference/organization/create-organization

## When to use

Use this skill when:
- Creating or updating patient records in a healthcare application
- Querying patient medical data from HIEs, pharmacies, or labs
- Retrieving consolidated FHIR-formatted patient data
- Generating medical record summaries (PDF/HTML)
- Sending secure clinical messages between providers
- Managing healthcare facilities and their associated patients
- Setting up webhook integrations to receive real-time data updates
- Contributing patient data back to health networks (required for compliance)
- Testing healthcare workflows in sandbox mode before production
- Managing patient cohorts for bulk operations or scheduled queries

## Quick reference

### API Authentication
Include API key in every request header:
```
x-api-key: YOUR_API_KEY
```

### Core Resource Operations

| Resource | Create | Read | Update | Delete | List |
|----------|--------|------|--------|--------|------|
| Patient | POST `/medical/v1/patient` | GET `/medical/v1/patient/{id}` | PUT `/medical/v1/patient/{id}` | DELETE `/medical/v1/patient/{id}` | GET `/medical/v1/patient` |
| Facility | POST `/medical/v1/facility` | GET `/medical/v1/facility/{id}` | PUT `/medical/v1/facility/{id}` | DELETE `/medical/v1/facility/{id}` | GET `/medical/v1/facility` |
| Cohort | POST `/medical/v1/cohort` | GET `/medical/v1/cohort/{id}` | PUT `/medical/v1/cohort/{id}` | DELETE `/medical/v1/cohort/{id}` | GET `/medical/v1/cohort` |

### Key Endpoints

| Task | Endpoint | Method |
|------|----------|--------|
| Query patient data from networks | POST `/medical/v1/network/query` | POST |
| Get consolidated FHIR data | POST `/medical/v1/fhir/consolidated-data` | POST |
| Get consolidated data status | GET `/medical/v1/fhir/consolidated-data/{id}` | GET |
| Generate medical record summary | POST `/medical/v1/fhir/consolidated-data` (with `conversionType: pdf\|html`) | POST |
| Send secure message | POST `/medical/v1/message` | POST |
| Get message status | GET `/medical/v1/message/{id}/status` | GET |
| Configure webhook | POST `/medical/v1/settings` | POST |
| Get webhook status | GET `/medical/v1/settings/webhook` | GET |

### Rate Limits

| Operation | Max per minute | Min interval |
|-----------|----------------|--------------|
| Patient Create/Update | 15 | 1 per 4 sec |
| Network Query Start | 20 | 1 per 3 sec |
| Consolidated Data Query | 120 | 1 per 0.5 sec |
| Send Message | 20 | 1 per 3 sec |

### Webhook Signature Validation (Node.js)
```javascript
import crypto from 'crypto';

function verifyWebhookSignature(key, body, signature) {
  const computed = crypto
    .createHmac('sha256', key)
    .update(body)
    .digest('hex');
  return crypto.timingSafeEqual(computed, signature);
}
```

## Decision guidance

| Scenario | Use Network Query | Use Consolidated Data Query |
|----------|-------------------|------------------------------|
| Need fresh data from external sources | ✓ | ✗ |
| Querying cached data from previous network query | ✗ | ✓ |
| First time retrieving patient data | ✓ | ✗ (after network query completes) |
| Polling for updates on existing data | ✗ | ✓ |

| Scenario | Use Webhooks | Use Polling |
|----------|--------------|------------|
| Real-time data delivery required | ✓ | ✗ |
| Asynchronous processing preferred | ✓ | ✗ |
| Simple synchronous flow | ✗ | ✓ |
| High-volume data transfers | ✓ | ✗ |

| Scenario | Use Dashboard | Use API |
|----------|---------------|---------|
| One-time setup or testing | ✓ | ✗ |
| Programmatic integration | ✗ | ✓ |
| Bulk operations | ✗ | ✓ |
| Manual patient/facility management | ✓ | ✗ |

## Workflow

### Typical patient data retrieval workflow

1. **Set up authentication**: Generate API key from dashboard (Developers page), store securely in environment variables, never commit to version control.

2. **Create facility**: POST to `/medical/v1/facility` with NPI number (use test NPI `1234567893` in sandbox), address, and contact info. Store returned facility ID.

3. **Create patient**: POST to `/medical/v1/patient` with demographics (name, DOB, address, phone, email), link to facility ID. Metriport auto-links to HIE data sources based on demographics.

4. **Configure webhook** (optional but recommended): POST to `/medical/v1/settings` with your public endpoint URL. Metriport generates webhook key for signature validation.

5. **Trigger network query**: POST to `/medical/v1/network/query` with patient ID, specify sources (hie, pharmacy, lab). Returns immediately with request ID; data arrives asynchronously.

6. **Receive webhook or poll**: If webhooks configured, Metriport calls your endpoint with `network-query.hie`, `network-query.pharmacy`, `network-query.lab` events. Otherwise, poll `/medical/v1/network/query/{id}` for status.

7. **Query consolidated data**: POST to `/medical/v1/fhir/consolidated-data` with patient ID and optional filters (resource types, date range). Returns cached result from network query.

8. **Download data**: Webhook or API response includes download URL (valid 10 minutes) to FHIR JSON, PDF, or HTML. For medical record summary, use `conversionType: pdf` or `html`.

9. **Contribute data back** (required): POST to `/medical/v1/fhir/consolidated-data` (create endpoint) or `/medical/v1/document` (upload) to return net-new clinical data to networks.

## Common gotchas

- **Network Query returns 2XX even on partial failures**: Always check the `errors` array in response body for source-level failures; don't rely on HTTP status codes alone.

- **Consolidated Data Query retrieves cached data only**: It does not fetch fresh data from external sources. Use Network Query first, then Consolidated Data Query after webhooks arrive or query completes.

- **Webhook signature validation is mandatory**: Validate `x-metriport-signature` header using HMAC-SHA256 before processing payload. Avoid parsing body before computing signature.

- **Webhook responses must be under 4 seconds**: Process asynchronously and respond with 200 immediately. Metriport will retry failed deliveries; use dashboard or API to manually retry.

- **API key rotation requires two keys active simultaneously**: Generate second key, deploy to all services, then revoke old key. Never have zero keys active.

- **Patient matching is automatic but not guaranteed**: Metriport links patients to HIE data based on demographics. Use Match Patient endpoint to search for existing patients before creating duplicates.

- **Data contribution is mandatory, not optional**: Failure to contribute net-new clinical data back to networks can result in access revocation. Exceptions exist for "OBO" (On Behalf Of) facilities already connected to networks.

- **Sandbox NPI is test-only**: Use `1234567893` for sandbox facilities only. Production requires real NPI number for covered entity.

- **Webhook URLs must be public and not redirect**: Metriport cannot follow HTTP redirects. Endpoint must be directly accessible from internet.

- **Metadata in webhooks is optional but useful**: Pass up to 50 key-value pairs (keys ≤40 chars, values ≤500 chars) when triggering queries; they return in webhook `meta.data` field for correlation.

- **Document download URLs expire in 10 minutes**: Cache or download immediately after receiving webhook; URLs are not permanent.

- **Cohorts are required for scheduled queries**: To enable automated daily/weekly/monthly queries, create cohorts and add patients to them.

## Verification checklist

Before submitting work with Metriport API:

- [ ] API key is stored in environment variables, not hardcoded
- [ ] Webhook signature validation is implemented (HMAC-SHA256 with `x-metriport-signature` header)
- [ ] Webhook endpoint responds with HTTP 200 within 4 seconds
- [ ] Webhook endpoint is idempotent (handles duplicate payloads safely)
- [ ] Network Query response is checked for `errors` array, not just HTTP status
- [ ] Consolidated Data Query is only called after Network Query completes (via webhook or polling)
- [ ] Patient creation includes facility ID and valid demographics
- [ ] Facility creation includes valid NPI (test NPI in sandbox, real NPI in production)
- [ ] Data contribution workflow is implemented (required for compliance)
- [ ] Rate limits are respected (check `medical-api/more-info/limits` for current limits)
- [ ] Error responses are handled per RFC 7807 format (status, name, title, detail fields)
- [ ] Sandbox mode is used for testing before production deployment
- [ ] Webhook retry logic is in place (manual retry via API or dashboard if needed)

## Resources

**Comprehensive navigation**: https://docs.metriport.com/llms.txt

**Critical documentation pages**:
1. [Medical API Quickstart](https://docs.metriport.com/medical-api/getting-started/quickstart) — Start here for end-to-end workflow
2. [API Reference](https://docs.metriport.com/medical-api/api-reference/organization/create-organization) — Complete endpoint documentation
3. [Webhooks Guide](https://docs.metriport.com/medical-api/getting-started/webhooks) — Webhook setup, authentication, and message types

---

> For additional documentation and navigation, see: https://docs.metriport.com/llms.txt