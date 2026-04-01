---
description: Comprehensive code review with actionable findings
argument-hint: file path, directory, or paste code
allowed-tools: Read, Grep, Glob, Bash(git diff:*)
---

# Code Review

Review the following code as a Principal Engineer. Be direct and specific.

```
$ARGUMENTS
```

## Review Priorities (in order)

1. **Correctness** - Logic errors, unhandled edge cases, race conditions, null safety
2. **Security** - Injection, auth gaps, data exposure, OWASP Top 10 violations
3. **Design** - Abstractions, coupling, cohesion, separation of concerns, SOLID violations
4. **Performance** - Algorithmic complexity, unnecessary allocations, N+1 queries, missing indexes
5. **Maintainability** - Readability, naming, complexity, testability

## Output Format

For each finding:
- **Location**: file:line or code snippet
- **Severity**: Critical / High / Medium / Low
- **Issue**: One-sentence description
- **Fix**: Concrete code change or approach

End with:
- **Verdict**: Ship / Ship with changes / Needs rework
- **Top 3 priorities** if changes are needed
