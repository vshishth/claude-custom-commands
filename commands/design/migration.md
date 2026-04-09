---
description: Generate safe database migration scripts
argument-hint: database type, current schema, and desired changes
allowed-tools: Read, Grep, Glob, Bash(psql:*, mysql:*, sqlite3:*, mongosh:*)
---

# Database Migration

Act as a Principal Engineer. Generate safe, zero-downtime migration scripts.

```
$ARGUMENTS
```

## Process

1. **Analyze** the current schema and the desired end state. If not provided, scan for migration files or ORM models in the codebase.
2. **Plan** the migration with zero-downtime in mind:
   - Can this be done without locking tables?
   - Does this need a multi-step deploy (add column → backfill → add constraint → drop old)?
   - Is the migration reversible?
   - Will it impact connection pool availability?
3. **Estimate timing** — For large tables (>1M rows), estimate execution time. If >30 seconds, require a batching strategy.
4. **Generate** both UP and DOWN migration scripts
5. **Define monitoring** — queries to track migration progress and detect issues during execution
6. **Validate** data integrity with pre/post-migration checks

## Output

- **UP migration script** — with inline comments explaining each step
- **DOWN migration script** — verified to fully reverse the UP migration
- **Pre-migration validation query** — confirms preconditions are met
- **Post-migration verification query** — confirms data integrity after migration
- **Estimated execution time** — based on table size assumptions
- **Monitoring queries** — to run during migration to track progress

## Safety Checklist

- [ ] Backward compatible with current application code
- [ ] No long-running locks on large tables
- [ ] Batched data backfills for large datasets (configurable batch size)
- [ ] Rollback script tested and verified
- [ ] Index creation uses CONCURRENTLY where supported
- [ ] Feature flag coordination — if app code depends on new schema, deploy behind a flag first
- [ ] Connection pool impact assessed — migration won't exhaust connections

## When Information is Insufficient

If current schema is not provided, scan the codebase for migration files or ORM models to reconstruct it. If table sizes are unknown, assume large (>1M rows) and design for zero-downtime. If the database type is unspecified, ask — migration safety varies significantly across databases.

## Constraints

- Every migration MUST have a working DOWN/rollback script
- Never add a NOT NULL column without a default in a single step — use multi-step: add nullable → backfill → add constraint
- Never drop a column that the current application version still references
- Backfill operations MUST be batched — never update millions of rows in a single transaction
