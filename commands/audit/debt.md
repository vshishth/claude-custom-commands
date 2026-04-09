---
description: Assess technical debt and create a prioritized paydown plan
argument-hint: directory, codebase area, or specific concern
allowed-tools: Read, Grep, Glob, Bash(wc:*, git log:*, git blame:*, cloc:*, npm:*, npx:*)
---

# Technical Debt Assessment

Act as a Principal Engineer. Assess technical debt and produce an actionable paydown plan.

```
$ARGUMENTS
```

## What to Look For

1. **Code debt** — Duplication, dead code, overly complex functions, poor naming, missing types
2. **Architecture debt** — Tight coupling, circular dependencies, god classes/modules, leaky abstractions
3. **Test debt** — Missing tests for critical paths, flaky tests, slow test suites, tests coupled to implementation
4. **Infrastructure debt** — Manual processes that should be automated, outdated tooling, missing CI checks
5. **Documentation debt** — Missing or stale docs for critical systems, undocumented tribal knowledge
6. **Velocity impact** — For each item, estimate how it slows the team (e.g., "every new feature takes 2x longer because of X")

## Output

For each debt item:
- **Area**: Where it lives (file:line or module)
- **Impact**: How it slows the team down (onboarding, bugs, deploy speed, etc.)
- **Effort**: S / M / L to address
- **Recommendation**: Fix now, plan for next quarter, or accept and document
- **Definition of Done**: What does "fixed" look like — specific and verifiable

**Summary section:**
- **Debt interest**: For the top 3 items, estimate ongoing cost if NOT addressed (in engineering time per sprint)
- **Quick wins**: High-impact, low-effort items suitable for tackling in a single sprint
- **Prioritized paydown plan**: Ordered by impact-to-effort ratio

## When Information is Insufficient

If the scope is "the whole project," focus on the top 10 highest-impact items. Do not attempt an exhaustive catalog — prioritize what matters most to team velocity.

## Constraints

- Every debt item MUST have a concrete "Definition of Done" — not vague "improve this"
- Prioritization MUST use impact-to-effort ratio, not just severity
- Do not modify any code — this is a read-only assessment
- Focus on debt that affects team velocity, not cosmetic issues
