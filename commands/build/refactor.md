---
description: Refactor code with a safe, incremental approach
argument-hint: file path or paste code to refactor
allowed-tools: Read, Grep, Glob, Bash(npm:*, npx:*, yarn:*, pnpm:*, pip:*, python:*, go:*, cargo:*, make:*, node:*, pytest:*, jest:*, vitest:*, tsc:*, eslint:*, git diff:*)
---

# Refactor

Act as a Principal Engineer. Analyze and refactor the following code. Preserve all existing behavior.

```
$ARGUMENTS
```

## Approach

1. **Identify** the specific problems: duplication, complexity, poor naming, tight coupling, missing abstractions, or SOLID violations
2. **Measure** — Capture before-state signals (cyclomatic complexity, duplication, line count) to quantify improvement
3. **Ensure test coverage** — If no tests cover the refactored code, write tests for the current behavior BEFORE refactoring
4. **Plan** an incremental sequence of safe transformations — each step should leave the code in a working state
5. **Execute** the refactoring with clear before/after for each change
6. **Validate** — Run existing tests to confirm nothing broke. Report before/after metrics.

## When Information is Insufficient

If no specific refactoring target is given, identify the highest-impact candidate in the specified file/directory using complexity and duplication as signals. If multiple issues exist, present a prioritized list and address the top one.

## Constraints

- Maximum scope: refactor one concern at a time. If >5 files need changes, present the plan for approval first.
- Each transformation must be small enough to review independently
- Do not change public interfaces unless explicitly requested
- Do not add speculative abstractions — only extract when duplication or complexity demands it
- Prioritize readability over cleverness
- Tests MUST pass after every transformation, not just at the end
