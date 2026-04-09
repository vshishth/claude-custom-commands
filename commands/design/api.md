---
description: Design APIs (REST or GraphQL) with contracts and documentation
argument-hint: domain model, requirements, or existing API to improve
allowed-tools: Read, Grep, Glob
---

# API Design

Act as a Principal Engineer. Design a production-grade API.

```
$ARGUMENTS
```

## Process

1. **Model resources** from the domain — identify entities, relationships, and operations
2. **Design endpoints/schema** following REST conventions or GraphQL best practices
3. **Define contracts** — request/response schemas, status codes, error format
4. **Address cross-cutting concerns**:
   - Authentication and authorization (scopes, permissions)
   - Pagination (cursor-based preferred for large datasets, include total count)
   - Filtering, sorting, and field selection
   - Rate limiting (quotas per tier, `Retry-After` header, 429 response body)
   - Versioning strategy (URL path vs header — recommend with justification)
   - Backward compatibility (additive-only changes, deprecation headers with sunset dates)

## Output

- **API specification** (OpenAPI/Swagger for REST, SDL for GraphQL)
- **Example requests and responses** for each endpoint, including error cases
- **Error contract** — consistent error response format with codes and machine-readable types
- **Authentication flow** — how clients authenticate and what scopes/permissions apply
- **Pagination strategy** — cursor-based preferred, with example response structure
- **Versioning approach** — chosen strategy with migration guidance
- **Backward compatibility notes** — what can change without breaking clients

## When Information is Insufficient

If the domain model is unclear, produce a resource model diagram first and ask the user to confirm before designing endpoints. If REST vs GraphQL is unspecified, recommend based on the use case (REST for CRUD-heavy, GraphQL for query-heavy with multiple consumers).

## Constraints

- Every endpoint MUST document error responses for 400, 401, 403, 404, and 500
- Never expose auto-increment IDs — use UUIDs or opaque identifiers
- Consistent naming conventions (plural nouns for REST resources, camelCase for fields)
- Validate all input at the boundary — specify exact validation rules per field
- Design for the client's use cases, not the database schema
- Idempotent operations where possible (include idempotency key for non-idempotent writes)
