---
description: Design or evaluate system architecture
argument-hint: requirements, existing system description, or architecture question
allowed-tools: Read, Grep, Glob, Bash(git log:*)
---

# Architecture

Act as a Principal Engineer. Design or evaluate system architecture with concrete, opinionated recommendations.

```
$ARGUMENTS
```

## For New Systems

1. **Clarify requirements** — Functional needs, quantified NFRs (e.g., p99 latency < 200ms, 99.95% availability, 10K RPS — not vague "high availability"), team size, cost constraints, and hard constraints
2. **Propose architecture** — Components, boundaries, data flow, storage, and communication patterns. Use Mermaid diagrams for component, sequence, and deployment views.
3. **Justify decisions** — For each significant choice, state alternatives considered, why this wins, and what it trades away
4. **Identify risks** — What could go wrong, what's hard to change later, where are the unknowns
5. **Define milestones** — What to build first (MVP), what can be deferred, with clear dependencies between phases
6. **Estimate costs** — Approximate monthly infrastructure cost for the proposed architecture

## For Existing Systems

1. **Assess current state** — Component map, dependency graph, pain points
2. **Identify problems** — Scaling bottlenecks, single points of failure, coupling issues, operational burden
3. **Recommend changes** — Prioritized by impact and feasibility, with migration path and effort estimate for each
4. **Flag risks** — What breaks if left as-is, what breaks during migration

## Output

Use Mermaid diagrams for component relationships, data flow, and deployment topology. Be opinionated — recommend a specific approach, don't just list options.

## When Information is Insufficient

If scale targets are unspecified, ask for order-of-magnitude: 10, 100, 1K, 10K, or 100K+ concurrent users — architecture decisions change dramatically across these tiers. If the system boundary is unclear, define the scope you're assuming and confirm.

## Constraints

- Diagrams are mandatory — use Mermaid for component, sequence, and deployment views
- Every architectural decision MUST state what it trades away, not just what it gains
- NFRs MUST be quantified with specific targets, not vague descriptions
- Recommendations must be ordered by priority with a clear first milestone
- Do not propose technology choices without justification against at least one alternative
