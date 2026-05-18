---
description: Generate API endpoint with handler, validation, tests, and route registration
argument-hint: endpoint description (e.g., "POST /api/reservations - create a new reservation")
allowed-tools: Read, Grep, Glob, Bash(go:*, npm:*, npx:*, tsc:*, mkdir:*, find:*)
---

# Generate Endpoint

Act as a Principal Engineer scaffolding a new API endpoint. Match the existing conventions in the codebase exactly — never impose external patterns.

Project type:
!`ls go.mod package.json Cargo.toml 2>/dev/null`

Existing routes:
!`grep -r "router\|HandleFunc\|app.get\|app.post\|@Get\|@Post\|Route\|Handle" --include="*.go" --include="*.ts" -l 2>/dev/null | head -10`

```
$ARGUMENTS
```

## Process

1. **Detect conventions** — Find existing endpoint handlers. Identify: file organization (by resource? by layer?), validation approach, error handling pattern, response format, middleware/interceptor usage.
2. **Generate handler** — Create the endpoint handler following discovered conventions. Include: input validation, business logic delegation (to a service layer), error handling, response formatting.
3. **Generate validation** — Add request validation matching the project's approach (struct tags, zod schemas, class-validator, etc.).
4. **Register route** — Add the route to the appropriate router/registration file.
5. **Generate tests** — Create handler tests covering: happy path, validation failure, service error, edge cases.

## When Information is Insufficient

If the endpoint description is incomplete, ask for: HTTP method, path, request/response shape, and which resource it belongs to. If no existing endpoints exist to copy conventions from, ask which framework to use or generate with standard patterns for the detected language.

## Output

Files created/modified:
- Handler file (path)
- Validation (if separate file)
- Route registration (path + line)
- Test file (path)

Each file with explanation of key decisions made.

## Constraints

- MUST match existing code conventions — do not introduce new patterns
- MUST include input validation for all user-provided data
- MUST include error handling that doesn't leak internal details
- MUST generate at least 3 test cases (happy path, bad input, error case)
- NEVER generate an endpoint without registering its route
- Use the project's existing test utilities and assertion style
