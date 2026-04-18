---
sources:
  - "[[Soft Deletion Probably Isn't Worth It]]"
  - "[[Clippings/The challenges of soft delete]]"
publish: true
tags: [evergreen]
similar:
  - Archive tables separate deleted data from live tables (0.80)
  - Soft deletes should use archive tables with triggers (0.80)
  - Easy, alternative soft deletion `deleted_record_insert` (0.80)
  - PostgreSQL triggers automate deletion archival (0.80)
  - Soft deletes should use separate archive tables with triggers (0.80)
compiled: 2026-04-06
---

Adding `deleted_at` columns to tables forces every query to include `WHERE deleted_at IS NULL` to filter out soft-deleted records. Forgetting this predicate accidentally exposes deleted data.

ORMs can hide this with default scopes (e.g., Rails' `acts_as_paranoid`), but this creates different problems:
- Manual database queries become dangerous (easy to forget the filter)
- Analytics queries become more complex
- Debugging requires remembering to check for deleted data

The complexity compounds with foreign keys. Soft-deleting a parent doesn't cascade to children, so you must manually track and soft-delete related records. The database can't enforce referential integrity on soft-deleted data.

GDPR compliance requires eventually hard-deleting old data. With `deleted_at`, this means elaborate multi-table CTEs to maintain foreign key relationships during cleanup—one project required a 30-table CTE.

**Related:** This is similar to how default scopes in Rails hide complexity that surfaces later in unexpected ways.
