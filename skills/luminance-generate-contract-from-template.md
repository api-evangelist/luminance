---
name: Generate a contract from a document template
description: Discover a Luminance document template, read its merge fields, generate a new contract (matter plus generated document), and verify the result.
api: openapi/luminance-public-api-v2-openapi-original.yml
api_version: '1.5'
operations:
  - GET /api2/projects
  - GET /api2/projects/{project_id}/document_templates
  - GET /api2/projects/{project_id}/document_templates/{document_template_id}
  - GET /api2/projects/{project_id}/document_templates/{document_template_id}/fields
  - POST /api2/projects/{project_id}/document_templates/create
  - GET /api2/projects/{project_id}/matters/{matter_id}
  - GET /api2/projects/{project_id}/matters/{matter_id}/versions
generated: '2026-08-04'
method: generated
source: openapi/luminance-public-api-v2-openapi-original.yml
---

# Generate a contract from a document template

This is Luminance's contract-creation flow: a template plus field values produces a **matter**
and a generated **document** in one call. Operations are identified by method and path because
the published spec carries no `operationId`.

## Before you start

Authenticate exactly as in `luminance-ingest-and-analyze-contract.md` — OAuth2 client
credentials against `https://{moniker}.app.luminance.com/auth/oauth2/token`, then a bearer
token on every call.

**This flow is not idempotent.** `POST .../document_templates/create` creates a matter and a
document with no deduplication key. If the call times out, do **not** blind-retry — search for
the matter by name first (step 6) and only retry if it is genuinely absent.

## Steps

1. **Pick the project.** `GET /api2/projects` → keep `id`.

2. **List templates.**
   `GET /api2/projects/{project_id}/document_templates`.
   Filter with `name` or `state`. Each template carries `default_folder_id` — the folder the
   generated document will be written to — and a Word `media_type`.

3. **Inspect one template.**
   `GET /api2/projects/{project_id}/document_templates/{document_template_id}` for its
   configuration `options`.

4. **Read the merge fields — do this before generating, every time.**
   `GET /api2/projects/{project_id}/document_templates/{document_template_id}/fields`.
   Each field returns `key` (the name on the template itself, which is what you supply),
   `name` (the display label), `datatype` (usually `generic:text`), `field_order` (top-to-bottom,
   left-to-right position) and `parent_data_field_id` (set when the field sits inside a nested
   loop — supply those as children, not as flat keys). `options` holds the permitted values for
   constrained fields. Never hard-code a field list; templates are customer-configured and
   change without any API changelog.

5. **Generate.**
   `POST /api2/projects/{project_id}/document_templates/create`, supplying the template id and
   the field values keyed by each field's `key`. A 200/201 means Luminance created a matter and
   generated the document into the template's `default_folder_id`.

6. **Verify.**
   `GET /api2/projects/{project_id}/matters/{matter_id}` confirms the matter, and
   `GET /api2/projects/{project_id}/matters/{matter_id}/versions` lists the generated version.
   A version's `type` is `attachment|draft|version` — the generated contract is a `version` or
   `draft`; `attachment` means supporting material outside the version history.

## Common failures

- **422** — a required field key is missing, or a value violates the field's `options` enum.
  The response carries no field-level detail, so re-read step 4 and diff your payload keys
  against the returned `key` values.
- **403** — the Service User has no contract-creation role on this project.
- **429** — 100 requests / 10 minutes across the instance. Cache the template field list.

## Related

- `data-model/luminance-data-model.yml` — how DocumentTemplates → DocumentTemplateFields →
  Matters → MatterVersion connect.
- `conventions/luminance-conventions.yml` — paging, error envelope, and the absent idempotency
  contract.
