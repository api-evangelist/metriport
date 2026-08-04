# Metriport (metriport)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Metriport is an open-source, universal API for healthcare data. The Medical API exchanges patient medical records across the CommonWell and Carequality networks and returns consolidated FHIR R4 data, while the Devices API hydrates activity, biometrics, nutrition, and sleep data from consumer wearables and mHealth apps. Companies can use the hosted Metriport cloud or self-host the open-source code to avoid vendor lock-in.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/metriport/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/metriport/refs/heads/main/apis.yml)

## Tags

- Healthcare
- Medical Records
- FHIR
- Health Data
- Wearables
- Open Source

## Timestamps

- **Created:** 2026-06-21
- **Modified:** 2026-06-21

## APIs

### Metriport Medical Patients API

Create, read, update, delete, list, and match patients tied to a facility, plus demographic matching and external-ID lookups, as the entry point for medical record exchange.

- **Human URL:** [https://docs.metriport.com/medical-api/api-reference/patient/create-patient](https://docs.metriport.com/medical-api/api-reference/patient/create-patient)
- **Base URL:** `https://api.metriport.com/medical/v1`

#### Tags

- Healthcare
- Patients
- FHIR

#### Properties

- [Documentation](https://docs.metriport.com/medical-api/api-reference/patient/create-patient)
- [API Reference](https://docs.metriport.com/medical-api/api-reference/patient/create-patient)
- [OpenAPI](openapi/metriport-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/metriport.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/metriport.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Metriport Medical Facilities API

Manage the facilities (care locations) under your organization where patients receive care, including create, get, list, update, and delete operations.

- **Human URL:** [https://docs.metriport.com/medical-api/api-reference/facility/create-facility](https://docs.metriport.com/medical-api/api-reference/facility/create-facility)
- **Base URL:** `https://api.metriport.com/medical/v1`

#### Tags

- Healthcare
- Facilities
- Organizations

#### Properties

- [Documentation](https://docs.metriport.com/medical-api/api-reference/facility/create-facility)
- [API Reference](https://docs.metriport.com/medical-api/api-reference/facility/create-facility)
- [OpenAPI](openapi/metriport-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/metriport.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/metriport.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Metriport Medical Document Query API

Trigger a network query for a patient's clinical documents across the HIE networks, list returned DocumentReferences, and retrieve signed download URLs for individual documents and bulk exports.

- **Human URL:** [https://docs.metriport.com/medical-api/api-reference/document/list-documents](https://docs.metriport.com/medical-api/api-reference/document/list-documents)
- **Base URL:** `https://api.metriport.com/medical/v1`

#### Tags

- Healthcare
- Documents
- C-CDA

#### Properties

- [Documentation](https://docs.metriport.com/medical-api/api-reference/document/list-documents)
- [API Reference](https://docs.metriport.com/medical-api/api-reference/document/list-documents)
- [OpenAPI](openapi/metriport-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/metriport.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/metriport.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Metriport Medical Consolidated FHIR API

Query and return a patient's consolidated, de-duplicated medical history as FHIR R4 (or PDF/HTML/AI medical record summary), count available resources, and contribute your own FHIR data back to the patient record.

- **Human URL:** [https://docs.metriport.com/medical-api/api-reference/fhir/consolidated-data-query-post](https://docs.metriport.com/medical-api/api-reference/fhir/consolidated-data-query-post)
- **Base URL:** `https://api.metriport.com/medical/v1`

#### Tags

- Healthcare
- FHIR
- Medical Records

#### Properties

- [Documentation](https://docs.metriport.com/medical-api/api-reference/fhir/consolidated-data-query-post)
- [API Reference](https://docs.metriport.com/medical-api/api-reference/fhir/consolidated-data-query-post)
- [OpenAPI](openapi/metriport-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/metriport.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/metriport.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Metriport Devices Users API

Register Metriport users, generate a Connect Token for the Connect Widget so end users can link wearables and mHealth apps (Apple Health, Fitbit, Garmin, Oura, WHOOP, Withings), and revoke or delete user connections.

- **Human URL:** [https://docs.metriport.com/devices-api/getting-started/connect-quickstart](https://docs.metriport.com/devices-api/getting-started/connect-quickstart)
- **Base URL:** `https://api.metriport.com`

#### Tags

- Wearables
- Users
- Connect

#### Properties

- [Documentation](https://docs.metriport.com/devices-api/getting-started/connect-quickstart)
- [API Reference](https://docs.metriport.com/devices-api/getting-started/connect-quickstart)
- [OpenAPI](openapi/metriport-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/metriport.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/metriport.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Metriport Devices Biometrics API

Retrieve normalized health data hydrated from connected devices - activity, biometrics, body, nutrition, and sleep - for a given user and date.

- **Human URL:** [https://docs.metriport.com/devices-api/getting-started/connect-quickstart](https://docs.metriport.com/devices-api/getting-started/connect-quickstart)
- **Base URL:** `https://api.metriport.com`

#### Tags

- Wearables
- Biometrics
- Health Data

#### Properties

- [Documentation](https://docs.metriport.com/devices-api/getting-started/connect-quickstart)
- [API Reference](https://docs.metriport.com/devices-api/getting-started/connect-quickstart)
- [OpenAPI](openapi/metriport-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/metriport.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/metriport.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Metriport Webhooks API

Configure the account webhook URL and key, check webhook delivery status, and retry failed webhook requests so document-query, consolidated-data, and devices-data events are delivered asynchronously to your application.

- **Human URL:** [https://docs.metriport.com/medical-api/api-reference/settings/get-settings](https://docs.metriport.com/medical-api/api-reference/settings/get-settings)
- **Base URL:** `https://api.metriport.com`

#### Tags

- Webhooks
- Events
- Settings

#### Properties

- [Documentation](https://docs.metriport.com/medical-api/api-reference/settings/get-settings)
- [API Reference](https://docs.metriport.com/medical-api/api-reference/settings/get-settings)
- [OpenAPI](openapi/metriport-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/metriport.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/metriport.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [GitHub Organization](https://github.com/metriport)
- [LinkedIn](https://www.linkedin.com/company/metriport)
- [Website](https://www.metriport.com)
- [Documentation](https://docs.metriport.com)
- [Plans](plans/metriport-plans-pricing.yml)
- [Rate Limits](rate-limits/metriport-rate-limits.yml)
- [Fin Ops](finops/metriport-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
