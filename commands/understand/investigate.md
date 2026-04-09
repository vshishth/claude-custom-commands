---
description: Investigate a bug from vague symptoms, logs, or error reports
argument-hint: error message, log snippet, bug report, or symptom description
allowed-tools: Read, Grep, Glob, Bash(git log:*, git blame:*, git diff:*, npm:*, node:*, python:*, go:*, cargo:*)
---

# Investigate

Act as a Principal Engineer. Investigate the following issue and identify the most likely root cause.

```
$ARGUMENTS
```

## Process

1. **Parse symptoms** — Extract the concrete signals: error messages, stack traces, affected endpoints, timing, frequency
2. **Generate hypotheses** — List 3-5 possible causes ranked by likelihood, based on the symptoms and codebase
3. **Gather evidence** — For each hypothesis, search the codebase for supporting or contradicting evidence (grep for error strings, read related code paths, check configs). Correlate across log sources if multiple log patterns are mentioned — look for timestamp alignment.
4. **Narrow down** — Eliminate hypotheses that don't fit the evidence. Identify the most likely cause.
5. **Recommend next steps** — What to check, test, or fix

## Output

- **Likely root cause**: The most probable explanation with supporting evidence
- **Evidence**: What you found in the code that supports this conclusion
- **Other possibilities**: Runner-up hypotheses and what would confirm/rule them out
- **Recommended fix**: If the cause is clear, suggest the minimal fix
- **How to verify**: Steps to confirm the diagnosis before fixing

## When Information is Insufficient

If symptoms are too vague to generate hypotheses, ask for: exact error text, when it started, frequency, and whether anything changed recently (deploys, config changes, dependency updates).

## Constraints

- Start broad, narrow systematically — don't jump to the first plausible cause
- Distinguish between correlation and causation
- If the evidence is inconclusive, say so — don't guess
- Rank hypotheses by both likelihood AND blast radius — a low-probability catastrophic cause deserves investigation
- This is investigation, not debugging — you may not have a reproducible case yet
