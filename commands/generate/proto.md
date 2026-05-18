---
description: Generate protobuf definitions and client/server stubs
argument-hint: service or message description (e.g., "ReservationService with CRUD operations")
allowed-tools: Read, Grep, Glob, Bash(find:*, protoc:*, buf:*, go:*, npm:*, mkdir:*, ls:*)
---

# Generate Protobuf

Act as a Principal Engineer designing gRPC service contracts. Produce clean, well-documented proto definitions that follow buf lint standards and organizational conventions.

Existing protos:
!`find . -name "*.proto" 2>/dev/null | head -15`

Proto tooling:
!`ls buf.yaml buf.gen.yaml buf.lock Makefile 2>/dev/null`

```
$ARGUMENTS
```

## Process

1. **Detect conventions** — Read existing `.proto` files for: package naming, option settings (go_package, java_package), import patterns, message naming style, field numbering strategy, comment style.
2. **Design messages** — Define request/response messages with appropriate field types. Use wrapper types for optional fields, repeated for lists, oneof for variants.
3. **Design service** — Define the RPC service with methods following the project's patterns (unary, server-streaming, etc.). Include standard methods where appropriate (Get, List, Create, Update, Delete).
4. **Generate stubs** — Run `buf generate` or `protoc` with the project's existing generation config to produce Go/TS stubs.
5. **Wire boilerplate** — If the project has a standard server registration pattern, generate the server implementation skeleton.

## When Information is Insufficient

If no existing protos exist, ask for: package name, target languages, and whether to use buf or raw protoc. If the service description is vague, propose a standard CRUD interface and confirm before generating.

## Output

- Proto file(s) created (path)
- Generated stubs (paths)
- Server skeleton (if applicable)
- Buf lint/breaking check results

## Constraints

- MUST pass `buf lint` (or project equivalent) with zero warnings
- MUST include comments on every service, method, and non-obvious field
- Field numbers MUST never be reused if this is an evolution of an existing proto
- NEVER use `google.protobuf.Any` without explicit justification
- Use well-known types (Timestamp, Duration, FieldMask) over custom equivalents
- Reserve field numbers 1-15 for frequently-set fields (smaller wire encoding)
