---
sources:
  - "[[Soft Deletion Probably Isn't Worth It]]"
  - "[[Easy, alternative soft deletion `deleted_record_insert`]]"
  - "[[Clippings/The challenges of soft delete]]"
publish: true
tags: [evergreen]
similar:
  - deleted_at columns create query complexity (0.81)
  - PostgreSQL triggers automate deletion archival (0.81)
  - Soft deletes should use separate archive tables with triggers (0.81)
  - Archive tables separate deleted data from live tables (0.81)
  - Soft Deletion Probably Isn't Worth It (0.79)
compiled: 2026-04-06
---

For soft deletion, use a single archive table that automatically captures deletions via PostgreSQL triggers.

Traditional `deleted_at` columns [[deleted_at columns create query complexity|create query complexity]], break foreign key integrity, and make pruning difficult. [[Archive tables separate deleted data from live tables]], keeping queries simple and foreign keys working.

[[PostgreSQL triggers automate deletion archival]] by converting deleted rows to JSONB and storing them in a generic `deleted_record` table. This requires no application code changes—just attach triggers to tables you want to archive.

**Quick reference:**

```sql
CREATE TABLE deleted_record (
    id uuid PRIMARY KEY,
    table_name TEXT NOT NULL,
    record_id TEXT NOT NULL,
    data JSONB NOT NULL,
    deleted_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

CREATE FUNCTION deleted_record_insert() RETURNS trigger
    LANGUAGE plpgsql AS $$
    BEGIN
        INSERT INTO deleted_record (table_name, record_id, data)
        VALUES (TG_TABLE_NAME, OLD.id, to_jsonb(OLD));
        RETURN OLD;
    END;
$$;

CREATE TRIGGER deleted_record_insert AFTER DELETE ON users
    FOR EACH ROW EXECUTE FUNCTION deleted_record_insert();
```

**Tradeoffs:** Undelete becomes harder (JSONB → table rows requires manual work), but undelete rarely happens in practice due to side effects (external APIs, blob storage, etc.).

**Related:** This pattern mirrors separating hot/cold data in distributed systems. Notably, multiple practitioners arrived at this solution independently—Brandur in 2022 and others since—which is strong signal it's a robust pattern rather than a one-off hack.
