---
description: Refactor code with a safe, incremental approach
argument-hint: file path or paste code to refactor
allowed-tools: Read, Grep, Glob, Bash
---

# Refactor

Analyze and refactor the following code. Preserve all existing behavior.

```
$ARGUMENTS
```

## Approach

1. **Identify** the specific problems: duplication, complexity, poor naming, tight coupling, missing abstractions, or SOLID violations
2. **Plan** an incremental sequence of safe transformations - each step should leave the code in a working state
3. **Execute** the refactoring with clear before/after for each change
4. **Validate** - describe how to verify nothing broke (existing tests, new tests, manual checks)

## Constraints

- Each transformation must be small enough to review independently
- Do not change public interfaces unless explicitly requested
- Do not add speculative abstractions - only extract when duplication or complexity demands it
- Prioritize readability over cleverness
