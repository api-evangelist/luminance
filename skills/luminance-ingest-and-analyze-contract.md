---
name: Ingest a contract and run Traffic Light Analysis
description: Upload a document into a Luminance project folder, start Traffic Light Analysis on it, then read back the annotations the analysis produced.
api: openapi/luminance-public-api-v2-openapi-original.yml
api_version: '1.5'
operations:
  - GET /api2/
  - GET /api2/projects
  - GET /api2/projects/{project_id}/folders
  - POST /api2/projects/{project_id}/folders
  - POST /api2/projects/{project_id}/folders/{folder_id}/upload
  - GET /api2/projects/{project_id}/folders/{folder_id}/documents
  - POST /api2/projects/{project_id}/documents/{document_id}/traffic_light_analysis
  - GET /api2/projects/{project_id}/documents/{document_id}/annotations
  - GET /api2/projects/{project_id}/documents/{document_id}/annotations/annotationText
generated: '2026-08-04'
method: generated
source: openapi/luminance-public-api-v2-openapi-original.yml
---

# Ingest a contract and run Traffic Light Analysis

Luminance publishes no `operationId` on any operation, so every step below is identified by
its **HTTP method and path**, exactly as they appear in the harvested spec. The overlay at
`overlays/luminance-public-api-v2-overlay.yaml` assigns deterministic ids if your tooling
requires them.

## Before you start

- **Host.** Every call goes to the customer's own instance: `https://{moniker}.app.luminance.com`.
  There is no shared data plane — `api.luminance.com` serves documentation only.
- **Token.** Base64-encode `<client-id>:<client-secret>` for a Service User, then
  `POST https://{moniker}.app.luminance.com/auth/oauth2/token` with
  `Authorization: Basic <encoded>`, `Content-Type: application/x-www-form-urlencoded` and body
  `grant_type=client_credentials`. Send the returned `access_token` as
  `Authorization: Bearer <access_token>` on every request. No scopes exist — what you can do is
  governed by the Service User's platform permissions and project roles.
- **Budget.** 100 requests per 10 minutes for the whole instance. Do not poll tightly (see
  step 5). A 429 carries no `Retry-After`, so back off exponentially on your own clock.
- **No idempotency.** There is no `Idempotency-Key`. A retried upload creates a *new*
  document version, it does not deduplicate. Only retry after confirming the first attempt
  did not land (step 4).

## Steps

1. **Confirm the contract version.** `GET /api2/` returns `version`, `api2_version` and
   `product`. If the instance reports a product version below 1.43.0 it is serving the older
   v1.3.0/v1.4.0 API and the `/api2` paths in this skill do not exist — switch to
   `openapi/luminance-api-v1-4-openapi-original.yml`.

2. **Find the project.** `GET /api2/projects` lists the projects this token can reach. Keep
   `id`. Note `permissions` (`none|preview|native`) — it controls whether you will later be
   allowed to download the file back.

3. **Find or create the destination folder.**
   `GET /api2/projects/{project_id}/folders` (filter with `name`, or `parent_id` to walk the
   hierarchy). If it does not exist, `POST /api2/projects/{project_id}/folders`.

4. **Upload the document.**
   `POST /api2/projects/{project_id}/folders/{folder_id}/upload`.
   Then confirm ingestion with
   `GET /api2/projects/{project_id}/folders/{folder_id}/documents` and read the document's
   `state`. Only `import_complete` or `import_extracted` means the file is usable.
   `import_pending` means keep waiting; `import_failure` and `upload_failure` are terminal —
   do not retry blindly, the file will version-chain under the same `version_group`.

5. **Start Traffic Light Analysis.**
   `POST /api2/projects/{project_id}/documents/{document_id}/traffic_light_analysis`.
   This returns **202 Accepted** — the work is asynchronous and there is **no webhook, callback
   or event stream**. Discover completion by polling step 6 on a slow interval (start at 30s
   and back off); polling faster will burn the 100-request budget without finishing sooner.

6. **Read the results.**
   `GET /api2/projects/{project_id}/documents/{document_id}/annotations`
   returns the typed findings. Filter with `type` (e.g. `contract:state`, `contracttype`,
   `definedterm:definition`, `language`) or with `roles`. Resolve an annotation's underlying
   text with
   `GET /api2/projects/{project_id}/documents/{document_id}/annotations/annotationText`,
   passing the annotation id(s); set `fullParagraph=true` to return the whole surrounding
   paragraph rather than just the tagged span.

7. **Resolve the vocabulary.** `GET /api2/annotation_types` maps each `annotation_type_id` to
   its `key`, `name` and `options`, and tells you via `pre_built` whether a concept is
   out-of-the-box Luminance or defined in this customer's instance. Cache it — it changes
   rarely and every annotation read depends on it.

## Failure handling

There is no error body schema anywhere in the Luminance specs, so branch on the status code
only (`errors/luminance-problem-types.yml`):

- **401** — token expired; re-run the client-credentials exchange.
- **403** — the Service User lacks the project role, not the OAuth scope. Escalate to a
  Luminance administrator; retrying will not help.
- **404** — wrong project/folder/document id, or the object is in another project.
- **422** — a parameter value is outside the enum the spec declares (check document `state`,
  `version_state`, task `type`).
- **429** — you exceeded 100 requests / 10 minutes. Back off; Luminance's own documented
  remedy is to contact support.

## Paging

Collections take `limit` (default 50) and `offset`. There is **no cursor, no `has_more` and
no total count** — if a page returns exactly `limit` rows you must assume there may be more
and advance `offset` until a short page comes back.
