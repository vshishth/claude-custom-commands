---
description: Generate safe database migration scripts
argument-hint: database type, current schema, and desired changes
allowed-tools: Read, Glob, Bash
---

# Database Migration

Generate migration scripts for:

```
$ARGUMENTS
```

## Process

1. **Analyze** the current schema and the desired end state
2. **Plan** the migration with zero-downtime in mind:
   - Can this be done without locking tables?
   - Does this need a multi-step deploy (add column -> backfill -> add constraint)?
   - Is the migration reversible?
3. **Generate** both UP and DOWN migration scripts
4. **Validate** data integrity with pre/post-migration checks

## Safety Checklist

- Backward compatible with current application code
- No long-running locks on large tables
- Batched data backfills for large datasets
- Rollback script tested and verified
- Index creation uses CONCURRENTLY where supported
