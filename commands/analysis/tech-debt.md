---
description: Assess technical debt and create a prioritized paydown plan
argument-hint: directory, codebase area, or specific concern
allowed-tools: Read, Grep, Glob, Bash
---

# Technical Debt Assessment

Assess technical debt in:

```
$ARGUMENTS
```

## What to Look For

1. **Code debt** - Duplication, dead code, overly complex functions, poor naming, missing types
2. **Architecture debt** - Tight coupling, circular dependencies, god classes/modules, leaky abstractions
3. **Test debt** - Missing tests, flaky tests, slow test suites, tests coupled to implementation
4. **Infrastructure debt** - Manual processes that should be automated, outdated tooling, missing CI checks
5. **Documentation debt** - Missing or stale docs for critical systems, undocumented tribal knowledge

## Output

For each debt item:
- **Area**: Where it lives
- **Impact**: How it slows the team down (onboarding, bugs, deploy speed, etc.)
- **Effort**: S / M / L to address
- **Recommendation**: Fix now, plan for next quarter, or accept and document

End with a prioritized paydown plan - what to tackle first based on impact-to-effort ratio.
