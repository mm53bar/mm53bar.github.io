---
sources:
  - "[[Soft Deletion Probably Isn't Worth It]]"
  - "[[Clippings/The challenges of soft delete]]"
publish: true
tags: [evergreen]
similar:
  - Soft deletes should use archive tables with triggers (0.81)
  - PostgreSQL triggers automate deletion archival (0.80)
  - deleted_at columns create query complexity (0.80)
  - Soft Deletion Probably Isn't Worth It (0.80)
  - Easy, alternative soft deletion `deleted_record_insert` (0.80)
compiled: 2026-04-06
---

Storing deleted records in a separate table (rather than flagging them with `deleted_at`) keeps live data clean and queries simple.

A single `deleted_record` table can store deleted rows from any table using JSONB:

```sql
CREATE TABLE deleted_record (
    id uuid PRIMARY KEY,
    table_name TEXT NOT NULL,
    record_id TEXT NOT NULL,
    data JSONB NOT NULL,
    deleted_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);
```

**Benefits:**
- Queries on live tables never need `WHERE deleted_at IS NULL`
- Foreign keys work normally—database enforces referential integrity on live data
- Indexes stay efficient (not bloated with deleted rows)
- Backups are smaller (main tables don't accumulate years of dead data)
- Pruning old archived data is trivial: `DELETE FROM deleted_record WHERE deleted_at < NOW() - '90 days'::interval`

**Tradeoff:** Archived data is less accessible (stored as JSONB, not queryable with normal joins). But 99% of archived data is never read. When needed for debugging or support, JSONB queries work fine.

**Related:** Similar to hot/cold data separation in distributed systems—optimize for the common case (live data queries).
