---
description: Implement a feature from a description, issue, or spec
argument-hint: feature description, GitHub issue URL, or spec
allowed-tools: Read, Grep, Glob, Bash(npm:*, npx:*, yarn:*, pnpm:*, pip:*, python:*, go:*, cargo:*, make:*, node:*, pytest:*, jest:*, vitest:*, tsc:*, eslint:*, git diff:*), mcp__github__get_issue
---

# Implement Feature

Act as a Principal Engineer. Implement the following with production-quality code.

```
$ARGUMENTS
```

## Process

1. **Understand** — Read the description/issue/spec. Identify acceptance criteria and scope boundaries. If a GitHub issue URL is provided, fetch it.
2. **Scope check** — If the feature requires changes to more than 8 files or touches more than 3 system boundaries, outline the plan for user approval before coding.
3. **Explore** — Find existing code that's relevant: similar features, utilities to reuse, patterns to follow, test conventions in use
4. **Plan** — Outline the changes needed: which files to modify/create, what the approach is, any edge cases to handle. If modifying existing public APIs, document breaking changes and migration path.
5. **Build** — Implement the feature following existing project conventions. Write minimal, clean code.
6. **Test** — Add tests covering the happy path and important edge cases, using the project's existing test framework and patterns
7. **Verify** — Run tests and lint to confirm everything works

## When Information is Insufficient

If acceptance criteria are missing, define them explicitly and confirm with the user before building. If the issue references external systems or APIs not in the codebase, ask for documentation or define the interface boundary.

## Constraints

- Follow existing patterns in the codebase — don't introduce new conventions
- Reuse existing utilities and abstractions before creating new ones
- Never introduce new dependencies without stating why existing tools are insufficient
- Keep the implementation minimal — build exactly what was asked for
- Write tests as you go, not as an afterthought
- If requirements are ambiguous, state your assumptions before coding
- Scope limit: if implementation grows beyond the plan, stop and re-scope with the user
