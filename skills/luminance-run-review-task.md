---
name: Run a review task and record outcomes
description: Create a Knowledge Bank from a template, list the documents a Luminance task is reviewing, record review outcomes, and read the analysis results.
api: openapi/luminance-public-api-v2-openapi-original.yml
api_version: '1.5'
operations:
  - GET /api2/projects/{project_id}/tasks
  - GET /api2/projects/{project_id}/tasks/{task_id}
  - POST /api2/projects/{project_id}/tasks/knowledge_bank_from_template
  - GET /api2/projects/{project_id}/tasks/{task_id}/reviews
  - POST /api2/projects/{project_id}/tasks/{task_id}/reviews
  - GET /api2/projects/{project_id}/tasks/{task_id}/reviews/{review_id}
  - PATCH /api2/projects/{project_id}/tasks/{task_id}/reviews/{review_id}
  - PATCH /api2/projects/{project_id}/tasks/{task_id}/reviews
  - GET /api2/projects/{project_id}/tasks/{task_id}/reviews/{review_id}/analysis
  - GET /api2/projects/{project_id}/tasks/{task_id}/reviews/documents
  - GET /api2/users/me
generated: '2026-08-04'
method: generated
source: openapi/luminance-public-api-v2-openapi-original.yml
---

# Run a review task and record outcomes

A Luminance **task** is a unit of review work; each document passing through it is a
**review**. `type: precedent` is what the Luminance UI calls a *Knowledge Bank*.

## Steps

1. **Identify yourself.** `GET /api2/users/me` returns the user behind the token. Reviews carry
   `assigned_to` and `outcome`, so know which user you are acting as before you write anything.

2. **List tasks.** `GET /api2/projects/{project_id}/tasks`, filtering with `type`
   (`task|precedent|alert|comparison`) or `name`. Read `auto_sync`: `true` means matching
   documents flow into the task automatically, `false` means they are staged and must be added,
   `null` means no sync at all — this determines whether step 4 is necessary.

3. **Create a Knowledge Bank when you need one.**
   `POST /api2/projects/{project_id}/tasks/knowledge_bank_from_template` builds a precedent
   task from a template and generates its positions. The `async` parameter is **required**:
   `true` returns **202 Accepted** and the task is built in the background; `false` blocks until
   the task exists. There is no callback — if you pass `async=true`, discover completion by
   re-listing tasks (step 2) on a slow interval.

4. **See what is in the task.**
   `GET /api2/projects/{project_id}/tasks/{task_id}/reviews` lists reviews;
   `GET /api2/projects/{project_id}/tasks/{task_id}/reviews/documents` lists the underlying
   documents. Filter reviews on `review_state` (`pending|complete`), `assigned_to` or `state`
   (`active`, `sync_staged` — flagged to appear but not yet added — or deleted).

5. **Add a document to the review set.**
   `POST /api2/projects/{project_id}/tasks/{task_id}/reviews`.

6. **Read the analysis.**
   `GET /api2/projects/{project_id}/tasks/{task_id}/reviews/{review_id}/analysis` returns
   Luminance's results for that document within that task — this is what you summarise, not the
   raw document.

7. **Record the outcome.**
   `PATCH /api2/projects/{project_id}/tasks/{task_id}/reviews/{review_id}` sets
   `review_state` and, for precedent (Knowledge Bank) tasks, `outcome` — the approval decision
   for that stage.

## Handle bulk updates carefully

`PATCH /api2/projects/{project_id}/tasks/{task_id}/reviews` (no `{review_id}`) updates **every
review matching the query filter**, and the sibling
`DELETE .../reviews/documents` removes every matching document from the task. These are
fan-out writes with:

- no dry-run or preview,
- no `Idempotency-Key` (a retry after a timeout re-applies the whole update),
- no count returned before the change.

Always run the equivalent `GET` with the identical filter first, confirm the size and identity
of the affected set, and prefer the single-`{review_id}` form when acting on behalf of a user.

## Failure handling

- **403** — the Service User lacks the project role for review writes; Luminance authorization
  is role-based, not scope-based, so no token change will fix it.
- **422** — `review_state` or `outcome` outside the values the spec declares.
- **429** — 100 requests / 10 minutes, instance-wide. Do not poll a 202 task build faster than
  every 30 seconds.

## Related

- `errors/luminance-problem-types.yml` — the full status-code catalogue (there is no error body
  schema).
- `conventions/luminance-conventions.yml` — the filter-scoped bulk-write hazard, paging, and
  the absent idempotency contract.
