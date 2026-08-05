---
name: Search the contract repository and read matter intelligence
description: Search Luminance for matters and documents, then read the typed annotations that carry the contract intelligence behind each result.
api: openapi/luminance-public-api-v2-openapi-original.yml
api_version: '1.5'
operations:
  - GET /api2/search
  - GET /api2/search/matters
  - GET /api2/search/documents
  - GET /api2/annotation_types
  - GET /api2/projects/{project_id}/matters
  - GET /api2/projects/{project_id}/matters/{matter_id}
  - GET /api2/projects/{project_id}/matters/{matter_id}/annotations
  - GET /api2/projects/{project_id}/matters/{matter_id}/relations
  - GET /api2/projects/{project_id}/matters/{matter_id}/events
  - GET /api2/projects/{project_id}/documents/{document_id}/annotations/annotationText
generated: '2026-08-04'
method: generated
source: openapi/luminance-public-api-v2-openapi-original.yml
---

# Search the contract repository and read matter intelligence

The read path an agent should use to answer questions about a customer's contracts. Search is
new in v1.5 ("Public API v2") — it does not exist in v1.3.0 or v1.4.0, so check
`GET /api2/` first and fall back to project-scoped listing if the instance is on an older
product version.

## Steps

1. **Load the vocabulary once.** `GET /api2/annotation_types` returns every concept the
   instance understands: `key`, `name`, `type` (`contract:state`, `contracttype`,
   `definedterm:definition`, `definedterm:use`, `language`, `alert`, `alias`,
   `generic:enum`, …), `options` for enumerated concepts, and `pre_built` (out-of-the-box
   Luminance vs. customer-defined). Every annotation you read later is meaningless without
   this map. Cache it — the 100-request / 10-minute budget is instance-wide.

2. **Search.**
   - `GET /api2/search` — aggregated across types.
   - `GET /api2/search/matters` — contracts/matters only.
   - `GET /api2/search/documents` — files only.
   Use the narrow endpoints when you know what you are after; the aggregated one costs the
   same request but returns a mixed result set you then have to classify.

3. **Or list directly when you already know the project.**
   `GET /api2/projects/{project_id}/matters`, filtering on `name`, `state`, `created_at` or
   `created_by`.

4. **Open a matter.** `GET /api2/projects/{project_id}/matters/{matter_id}`.

5. **Read the intelligence.**
   `GET /api2/projects/{project_id}/matters/{matter_id}/annotations` returns the typed
   tag/value pairs — dates, parties, contract type, governing law, renewal terms, alerts —
   each keyed by `annotation_type_id`. Join to step 1 to turn ids into meaning. Filter with
   `annotation_type_id` or `state` (`active|deleted`); **always filter to `active`** unless
   you specifically want deleted tags.

6. **Follow the contract graph.**
   `GET /api2/projects/{project_id}/matters/{matter_id}/relations` returns directed
   `source_id → target_id` links between matters (amendments, parent agreements, related
   contracts). `GET .../events` returns the matter's activity history.

7. **Quote the source text.** For a document-level annotation, resolve the underlying wording
   with `GET /api2/projects/{project_id}/documents/{document_id}/annotations/annotationText`,
   passing the annotation id (repeat the parameter for several). Set `fullParagraph=true` when
   the clause matters more than the tagged span — this is what you cite, rather than
   paraphrasing an annotation value.

## Rules an agent must respect

- **Never claim a total.** Collections return `limit` (default 50) and `offset` with no
  `has_more` and no count. A full page means "possibly more" — advance `offset` until a short
  page returns, and say "at least N" if you stop early.
- **Stay inside the project boundary.** Ids are bare integers with no type prefix, so a
  document id from one project will 404 (or, worse, silently resolve to the wrong object shape)
  in another. Always carry `project_id` alongside any id.
- **Read-only means read-only.** This skill uses only GET. The bulk `PATCH`/`DELETE`
  filter-scoped endpoints on folders, matters and documents act on an entire filtered set with
  no dry-run and no idempotency key — never invoke them from a search flow.
- **Budget.** 100 requests / 10 minutes for the whole instance, shared with every other
  integration. Batch by filtering server-side rather than listing and filtering locally.

## Related

- `data-model/luminance-data-model.yml` — the Matter / MatterVersion / MatterRelation /
  Annotation graph.
- `conventions/luminance-conventions.yml` — paging, filtering and error semantics.
