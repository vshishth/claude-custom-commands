---
description: Create an Architecture Decision Record
argument-hint: decision topic or question to resolve
allowed-tools: Read, Grep, Glob
---

# Architecture Decision Record

Act as a Principal Engineer. Create a well-structured ADR that captures the decision and its context.

```
$ARGUMENTS
```

## Process

1. **Scan for existing ADRs** in the project — check `docs/adr/`, `docs/decisions/`, `ADR-*.md`, or similar patterns
2. **Determine the next ADR number** based on existing records
3. **Generate the ADR** following the format below

## Format

### Title
ADR-NNN: [Decision title in imperative form]

### Status
Proposed | Accepted | Deprecated | Superseded by ADR-NNN

### Context
What is the issue that motivates this decision? What forces are at play (technical, business, team)? Be specific about constraints and triggers.

### Decision
What is the change that we're proposing or have agreed to implement?

### Consequences
What becomes easier or harder because of this decision? MUST include at least one positive AND one negative consequence — every decision has tradeoffs.

### Alternatives Considered
What other options were evaluated? Why were they rejected? Each must have specific technical reasoning, not just "we preferred X."

### Impact Assessment
What systems, teams, or processes are affected by this decision?

### Review Date
When should this decision be revisited? (e.g., "Review in 6 months" or "Review if traffic exceeds 10K RPS")

## When Information is Insufficient

If the decision topic is broad, narrow it to a single binary or ternary choice. ADRs record ONE decision, not an entire architecture. If context is missing, list what context is needed before a decision can be made and set status to "Proposed."

## Constraints

- One ADR, one decision — if multiple decisions are intertwined, create separate ADRs and cross-link
- Consequences MUST include at least one negative consequence — no decision is purely positive
- Superseding ADRs MUST link to the ADR they replace
- Be concise — one page is ideal
- Focus on the WHY, not just the WHAT
- Link to relevant technical specs, PRs, or discussions
