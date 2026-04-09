---
sources:
  - "[[Easy, alternative soft deletion `deleted_record_insert`]]"
  - "[[Clippings/The challenges of soft delete]]"
publish: true
tags: [evergreen]
similar:
  - Archive tables separate deleted data from live tables (0.81)
  - Soft deletes should use archive tables with triggers (0.80)
  - deleted_at columns create query complexity (0.80)
  - Soft Deletion Probably Isn't Worth It (0.79)
  - Soft deletes should use separate archive tables with triggers (0.79)
compiled: 2026-04-06
---

PostgreSQL triggers can automatically capture deleted rows and store them in an archive table, requiring zero application code changes.

Create a generic trigger function that converts any deleted row to JSONB:

```sql
CREATE FUNCTION deleted_record_insert() RETURNS trigger
    LANGUAGE plpgsql AS $$
    BEGIN
        INSERT INTO deleted_record (table_name, record_id, data)
        VALUES (TG_TABLE_NAME, OLD.id, to_jsonb(OLD));
        RETURN OLD;
    END;
$$;
```

Attach it to any table:

```sql
CREATE TRIGGER deleted_record_insert AFTER DELETE ON users
    FOR EACH ROW EXECUTE FUNCTION deleted_record_insert();
```

The trigger uses `TG_TABLE_NAME` (the source table) and `OLD` (the deleted row) to automatically populate the archive. No need to modify application deletion logic.

For more sophisticated needs, track *why* records were deleted (direct vs. cascade) using session variables and an extended schema:

```sql
CREATE TABLE archive (
    id UUID PRIMARY KEY,
    table_name TEXT NOT NULL,
    record_id TEXT NOT NULL,
    data JSONB NOT NULL,
    archived_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    caused_by_table TEXT,
    caused_by_id TEXT
);
```

This lets you answer: "Which child records were deleted when user X was deleted?" — useful for audit trails and GDPR deletion verification.

**Evolution:** This pattern started with manual CTEs (`WITH deleted AS (DELETE ... RETURNING *)`) but triggers eliminate that boilerplate and ensure consistency—you can't accidentally delete without archiving.

**Tradeoff:** Adds minimal overhead to deletes, but [[Archive tables separate deleted data from live tables|live table queries improve overall]].
