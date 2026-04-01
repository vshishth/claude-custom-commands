---
description: Design or evaluate system architecture
argument-hint: requirements, existing system description, or architecture question
allowed-tools: Read, Grep, Glob, Bash
---

# Architecture

Design or evaluate the system architecture based on:

```
$ARGUMENTS
```

## For New Systems

1. **Clarify requirements** - Functional needs, scale targets, latency/throughput SLAs, team size, and constraints
2. **Propose architecture** - Components, boundaries, data flow, storage, and communication patterns
3. **Justify decisions** - For each significant choice, state the alternatives considered and why this wins
4. **Identify risks** - What could go wrong, what's hard to change later, where are the unknowns
5. **Define milestones** - What to build first, what can be deferred

## For Existing Systems

1. **Assess current state** - Component map, dependency graph, pain points
2. **Identify problems** - Scaling bottlenecks, single points of failure, coupling issues, operational burden
3. **Recommend changes** - Prioritized by impact and feasibility, with migration path for each
4. **Flag risks** - What breaks if left as-is, what breaks during migration

## Output

Use text-based diagrams (Mermaid or ASCII) for component relationships and data flow. Be opinionated - recommend a specific approach, don't just list options.
