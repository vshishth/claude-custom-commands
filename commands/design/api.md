---
description: Design APIs (REST or GraphQL) with contracts and documentation
argument-hint: domain model, requirements, or existing API to improve
allowed-tools: Read, Grep, Glob
---

# API Design

Design an API based on:

```
$ARGUMENTS
```

## Process

1. **Model resources** from the domain - identify entities, relationships, and operations
2. **Design endpoints/schema** following REST conventions or GraphQL best practices
3. **Define contracts** - request/response schemas, status codes, error format
4. **Address cross-cutting concerns**: authentication, pagination, filtering, rate limiting, versioning

## Output

- **API specification** (OpenAPI/Swagger for REST, SDL for GraphQL)
- **Example requests and responses** for each endpoint
- **Error contract** - consistent error response format with codes
- **Authentication flow** - how clients authenticate and what scopes/permissions apply
- **Pagination strategy** - cursor-based preferred for large datasets

## Principles

- Consistent naming conventions (plural nouns for REST resources)
- Idempotent operations where possible
- Validate all input at the boundary
- Don't expose internal IDs or implementation details
- Design for the client's use cases, not the database schema
