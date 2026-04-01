---
description: Write a technical design document for a feature or system
argument-hint: feature requirements or problem statement
allowed-tools: Read, Grep, Glob
---

# Technical Design Document

Write a technical design document based on:

```
$ARGUMENTS
```

## Structure

1. **Problem statement** - What problem are we solving and why now
2. **Goals & non-goals** - Explicitly scope what this does and does not address
3. **Proposed design** - Architecture, data model, API contracts, key algorithms
4. **Alternatives considered** - What else was evaluated and why the proposed approach wins
5. **Risks & mitigations** - What could go wrong, how we handle it
6. **Rollout plan** - How to ship incrementally with feature flags, migrations, or phased releases
7. **Observability** - What metrics, logs, and alerts confirm this works in production
8. **Open questions** - Decisions that still need input

Use diagrams (Mermaid) where they add clarity. Be specific enough that another engineer could implement this without ambiguity.
