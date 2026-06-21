# Metriport (metriport)

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
