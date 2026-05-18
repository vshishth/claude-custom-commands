---
description: Distributed trace analysis across multi-service hops
argument-hint: trace ID, error message, or service interaction to trace
allowed-tools: Read, Grep, Glob, Bash(grep:*, find:*, git log:*, git blame:*, curl:*)
---

# Distributed Trace Analysis

Act as a Principal Engineer debugging a distributed system. Trace request flow across service boundaries, identify where failures or latency originate.

Service structure:
!`find . -name "*.proto" -o -name "openapi*.yaml" -o -name "swagger*.json" | head -10 2>/dev/null`

Instrumentation:
!`grep -rl "otel\|opentelemetry\|tracing\|span" --include="*.go" --include="*.ts" -l 2>/dev/null | head -10`

```
$ARGUMENTS
```

## Process

1. **Map the request path** — From the entry point (API gateway, HTTP handler, gRPC server), trace the full call chain through interceptors, middleware, service calls, and database queries.
2. **Identify instrumentation** — Find where spans are created, what attributes are set, and where context propagation happens (or breaks).
3. **Locate failure points** — For the given trace ID or error, identify which hop introduced the failure. Check error handling, retries, timeouts, and circuit breakers.
4. **Analyze latency** — Identify which hops contribute most latency. Check for N+1 calls, missing concurrency, or serial calls that could be parallel.
5. **Verify propagation** — Confirm trace context (W3C traceparent, B3, or custom) is propagated correctly across all boundaries (HTTP headers, gRPC metadata, queue message attributes).

## When Information is Insufficient

If no trace ID is provided, analyze the instrumentation code and report gaps. If the trace spans multiple repos, analyze what's visible in the current repo and document the expected upstream/downstream contracts. If no instrumentation exists, recommend where to add it.

## Output

### Request Flow
```
Client → [Service A: handler] → [Service B: gRPC] → [Database]
         12ms                    45ms                  8ms
```

### Findings
- Where the issue occurs (service, file, line)
- Root cause (timeout, missing retry, broken propagation, etc.)
- Concrete fix with code location

### Instrumentation Gaps
- Missing spans, un-propagated context, missing error recording

## Constraints

- NEVER guess at service interactions — derive from code (imports, client instantiation, proto definitions)
- Distinguish between observed behavior (from traces/logs) and inferred behavior (from code analysis)
- Always check for context propagation at every boundary crossing
- Report uninstrumented hops as risks, not assumptions
