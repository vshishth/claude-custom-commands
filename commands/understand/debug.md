---
description: Systematic root cause analysis and debugging
argument-hint: error message, stack trace, or description of the bug
allowed-tools: Read, Grep, Glob, Bash(npm:*, node:*, python:*, go:*, cargo:*, git log:*, git blame:*, git diff:*)
---

# Debug

Act as a Principal Engineer. Diagnose the following issue systematically.

```
$ARGUMENTS
```

## Process

1. **Assess severity** — Is this a crash, data corruption, security issue, or UX annoyance? This determines urgency and approach.
2. **Reproduce** — Identify exact conditions that trigger the bug
3. **Isolate** — Narrow down to the specific component/line causing the failure
4. **Timeline** — Check `git log` and `git blame` for recent changes to the affected area. When was this introduced?
5. **Root cause** — Determine WHY the bug exists, not just WHERE
6. **Fix** — Provide the minimal correct fix
7. **Verify** — Suggest how to confirm the fix works and doesn't regress

## Output

- **Severity**: Crash / Data corruption / Security / Functional / UX
- **Root cause**: Clear explanation of why this happens
- **Blast radius**: What else might be affected by this bug or its fix
- **Fix**: Specific code changes with reasoning
- **Test**: How to verify the fix (specific test case or manual steps)
- **Prevention**: What would have caught this earlier (test, lint rule, type check, etc.)

## When Information is Insufficient

If the error message or stack trace is incomplete, list what additional information is needed to diagnose (full logs, reproduction steps, environment details). Do not guess without evidence — state what you know and what remains uncertain.

## Constraints

- Find the root cause, not just a workaround
- Minimal fix — don't refactor surrounding code while fixing a bug
- If the fix could affect other code paths, identify and document the blast radius
- If the bug is in a dependency, identify the exact version and recommend pinning or patching
