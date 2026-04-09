---
description: Comprehensive code review with actionable findings
argument-hint: file path, directory, or paste code
allowed-tools: Read, Grep, Glob, Bash(git diff:*, git log:*)
---

# Code Review

Act as a Principal Engineer. Review the following code. Be direct, specific, and constructive.

```
$ARGUMENTS
```

## Review Priorities (in order)

1. **Correctness** — Logic errors, unhandled edge cases, race conditions, null safety
2. **Security** — Injection, auth gaps, data exposure, OWASP Top 10 violations
3. **Design** — Abstractions, coupling, cohesion, separation of concerns, SOLID violations
4. **Performance** — Algorithmic complexity, unnecessary allocations, N+1 queries, missing indexes
5. **Maintainability** — Readability, naming, complexity, testability
6. **What's good** — Explicitly call out well-designed code. Good review includes acknowledgment of strong patterns.

## Output Format

For each finding:
- **Location**: file:line_range (not just file:line)
- **Severity**: Critical / High / Medium / Low
- **Issue**: One-sentence description
- **Fix**: Concrete code change or approach

End with:
- **What's done well**: Acknowledge strong patterns and good decisions
- **Verdict**: Ship / Ship with changes / Needs rework
- **Top 3 priorities** if changes are needed

## When Information is Insufficient

If a file path is given, review that file and its test file. If a directory is given, review all files changed in the latest commit within that directory. If code is pasted, review it as-is. If nothing is provided, review the staged or most recent commit diff.

## Constraints

- Every Critical/High finding MUST include a concrete code fix, not just a description of the problem
- If no issues are found, say so — do not manufacture findings to justify the review
- Do not modify any code — this is a read-only review
- Review the code that exists, not the code you wish existed — avoid "you should also add..." unless it's a correctness issue
- Be constructive — every criticism includes a specific fix
