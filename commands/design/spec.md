---
description: Write a technical design document for a feature or system
argument-hint: feature requirements or problem statement
allowed-tools: Read, Grep, Glob
---

# Technical Design Document

Act as a Principal Engineer. Write a technical design document that another engineer could implement without ambiguity.

```
$ARGUMENTS
```

## Structure

1. **Problem statement** — What problem are we solving and why now? Include the trigger or business driver.
2. **Goals & non-goals** — Explicitly scope what this does and does not address.
3. **Success metrics** — How do we know this worked? Quantify where possible (latency, throughput, adoption, error reduction).
4. **Proposed design** — Architecture, data model, API contracts, key algorithms. Use Mermaid diagrams for architecture and data flow.
5. **Alternatives considered** — What else was evaluated and why the proposed approach wins. Every alternative MUST explain why it was rejected, not just list it.
6. **Dependencies** — External teams, services, or decisions this blocks on. Flag anything that could delay delivery.
7. **Risks & mitigations** — What could go wrong, how we handle it. Include both technical and operational risks.
8. **Rollout plan** — How to ship incrementally: feature flags, phased rollout percentages, migrations, rollback triggers.
9. **Observability** — What metrics, logs, and alerts confirm this works in production. Include dashboard and alert definitions.
10. **Open questions** — Decisions that still need input. Each must be actionable (answerable by a specific person/team), not rhetorical.

## When Information is Insufficient

If requirements are vague, produce the "Open Questions" section first listing what must be answered before design can proceed. Do not invent requirements — surface the gaps. If the scope is too large for a single doc, recommend splitting into multiple specs.

## Output

Produce the complete design document following the structure above. Be specific enough that another engineer could implement this without further clarification.

## Constraints

- Diagrams are mandatory for architecture and data flow — use Mermaid
- Every alternative MUST explain why it was rejected with specific technical reasoning
- Open questions MUST be answerable and assigned to a person or team if known
- Success metrics MUST be quantified, not vague ("reduce errors by 50%" not "improve reliability")
