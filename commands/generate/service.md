---
description: Scaffold a new microservice with standard structure (Go gRPC or TS)
argument-hint: service name and type (e.g., "reservation-service grpc go", "notification-worker ts")
allowed-tools: Read, Grep, Glob, Bash(go:*, npm:*, mkdir:*, cp:*, find:*, ls:*, git init:*)
---

# Generate Service

Act as a Principal Engineer scaffolding a new microservice. Copy conventions from existing services in the workspace — never impose patterns that don't exist here.

Existing services (to copy conventions from):
!`find . -maxdepth 2 -name "main.go" -o -name "cmd" -type d | head -10 2>/dev/null`
!`find . -maxdepth 2 -name "package.json" | head -10 2>/dev/null`

Infrastructure patterns:
!`ls -d */deploy/ */helm/ */kubernetes/ 2>/dev/null | head -5`

```
$ARGUMENTS
```

## Process

1. **Detect conventions** — Scan existing services for: directory layout, config loading pattern, middleware/interceptor chain, health endpoints, graceful shutdown, Dockerfile structure, helm chart structure.
2. **Scaffold structure** — Generate the directory tree matching discovered conventions. Include: `cmd/`, `internal/`, `pkg/` (Go) or `src/`, `test/` (TS).
3. **Generate core files** — Create: main entrypoint with graceful shutdown, config loading, health endpoints (`/healthz`, `/readyz`), Dockerfile (multi-stage), basic CI config.
4. **Wire observability** — Include: structured logging, metrics endpoint, trace initialization (matching the stack used by siblings).
5. **Generate deploy config** — Create: Dockerfile, helm chart or docker-compose entry, matching the existing deploy patterns.

## When Information is Insufficient

If no existing services exist to copy from, ask for: language (Go/TS), type (gRPC/REST/worker), and preferred framework. If the service name is missing, ask for it. If deploy infrastructure is unclear, generate Dockerfile only and note that deploy config needs manual wiring.

## Output

### Generated Structure
```
service-name/
├── cmd/server/main.go
├── internal/
├── deploy/
├── Dockerfile
└── ...
```

### Files Created (list with one-line descriptions)
### Next Steps (what the developer must do manually)

## Constraints

- MUST include health endpoints from day 1 — no service without `/healthz` and `/readyz`
- MUST include graceful shutdown handling
- MUST include Dockerfile with multi-stage build
- MUST match existing service conventions (if detected) — consistency over preference
- NEVER generate a service without structured logging setup
- Include a README.md with build/test/run/deploy instructions
