---
description: Generate data models with migrations, repository layer, and validation
argument-hint: model description (e.g., "Reservation with guest_name, party_size, datetime, status")
allowed-tools: Read, Grep, Glob, Bash(go:*, npm:*, npx:*, find:*, mkdir:*, ls:*)
---

# Generate Model

Act as a Principal Engineer designing a data model. Generate the model definition, database migration, repository layer, and validation — all matching existing conventions.

ORM/database patterns:
!`grep -rl "gorm\|sqlx\|pgx\|prisma\|typeorm\|sequelize\|knex\|migrate" --include="*.go" --include="*.ts" --include="*.json" -l 2>/dev/null | head -10`

Existing models:
!`find . -path "*/model*" -o -path "*/entity*" -o -path "*/schema*" | grep -v node_modules | head -10 2>/dev/null`

```
$ARGUMENTS
```

## Process

1. **Detect ORM/migration conventions** — Identify the database layer: raw SQL, GORM, sqlx, Prisma, TypeORM, etc. Find existing models to copy patterns from.
2. **Generate model struct/type** — Define the model with appropriate types, tags (json, db, validate), and relationships. Match naming conventions from existing models.
3. **Generate migration** — Create a migration file using the project's migration tool (golang-migrate, goose, prisma migrate, knex, etc.) with proper up/down.
4. **Generate repository** — Create the data access layer with standard CRUD operations matching existing repository patterns (interface + implementation).
5. **Generate validation** — Add validation rules matching the project's approach (struct tags, zod schemas, class-validator decorators).

## When Information is Insufficient

If the model fields are incomplete, ask for: field names, types, required/optional, and relationships to other models. If no ORM is detected, ask which database approach to use. If no existing models exist, ask for conventions preference.

## Output

### Files Created
- Model: [path]
- Migration: [path]
- Repository: [path]
- Validation: [path] (if separate)

### Migration SQL
```sql
-- Up migration preview
```

### Usage Example
```
// How to use the generated repository
```

## Constraints

- MUST include both up AND down migrations — never generate irreversible migrations without warning
- MUST include created_at/updated_at timestamps (or equivalent) unless explicitly told not to
- MUST match existing field naming conventions (snake_case vs camelCase)
- NEVER generate models without validation for user-facing fields
- Include indexes for fields that will be queried frequently (foreign keys, status, timestamps)
- Soft deletes if the project uses them (detect from existing models)
