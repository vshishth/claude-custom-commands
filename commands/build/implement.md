---
description: Implement a feature from a description, issue, or spec
argument-hint: feature description, GitHub issue URL, or spec
allowed-tools: Read, Grep, Glob, Bash, mcp__github__get_issue
---

# Implement Feature

Implement the following:

```
$ARGUMENTS
```

## Process

1. **Understand** — Read the description/issue/spec. Identify acceptance criteria and scope boundaries. If a GitHub issue URL is provided, fetch it.
2. **Explore** — Find existing code that's relevant: similar features, utilities to reuse, patterns to follow, test conventions in use
3. **Plan** — Outline the changes needed: which files to modify/create, what the approach is, any edge cases to handle
4. **Build** — Implement the feature following existing project conventions. Write minimal, clean code.
5. **Test** — Add tests covering the happy path and important edge cases, using the project's existing test framework and patterns
6. **Verify** — Run tests and lint to confirm everything works

## Principles

- Follow existing patterns in the codebase — don't introduce new conventions
- Reuse existing utilities and abstractions before creating new ones
- Keep the implementation minimal — build exactly what was asked for
- Write tests as you go, not as an afterthought
- If requirements are ambiguous, state your assumptions before coding
