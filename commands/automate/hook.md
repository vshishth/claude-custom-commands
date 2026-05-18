---
description: Set up git hooks (pre-commit, pre-push, commit-msg) per project type
argument-hint: hook type or "all" (e.g., "pre-commit", "all", "remove")
allowed-tools: Read, Grep, Glob, Bash(git config:*, chmod:*, mkdir:*, find:*, ls:*, cat:*)
---

# Git Hook Setup

Act as a Principal Engineer configuring git hooks for quality enforcement. Generate project-appropriate hooks based on the detected stack.

Project type:
!`ls go.mod package.json Cargo.toml Makefile .golangci.yml .eslintrc* tsconfig.json 2>/dev/null`

Existing hooks:
!`ls .git/hooks/ .githooks/ .husky/ 2>/dev/null | head -10`

Test commands:
!`grep -A2 '"test"\|"lint"\|"typecheck"' package.json 2>/dev/null || grep -E "^(test|lint|check):" Makefile 2>/dev/null`

```
$ARGUMENTS
```

## Process

1. **Detect stack** — Identify language, linter, test runner, and formatter from project config files.
2. **Generate hooks** — Create appropriate hooks based on stack:
   - **pre-commit**: lint + format + type-check (fast checks only)
   - **pre-push**: full test suite (slower, runs before push)
   - **commit-msg**: conventional commit format enforcement
3. **Install mechanism** — Set up `.githooks/` directory and configure `git config core.hooksPath .githooks`. This is portable and doesn't require npm dependencies.
4. **Make executable** — Set proper permissions (`chmod +x`) on all hook files.
5. **Verify** — Test each hook with a dry run to confirm it works.

## When Information is Insufficient

If the test/lint commands can't be auto-detected, ask the user. If "remove" is specified, remove the hooks directory and reset `core.hooksPath`. If the project already uses Husky or lefthook, integrate with the existing system instead of replacing it.

## Output

### Hooks Generated
| Hook | Checks | Estimated Time |
|------|--------|---------------|
| pre-commit | lint, format, type-check | ~5s |
| pre-push | test suite | ~30s |
| commit-msg | conventional commit format | <1s |

### Files Created
- `.githooks/pre-commit`
- `.githooks/pre-push`
- `.githooks/commit-msg`

### Activation Command
```bash
git config core.hooksPath .githooks
```

## Constraints

- NEVER install hooks that take more than 10 seconds in pre-commit — move slow checks to pre-push
- ALWAYS include a bypass instruction (`git commit --no-verify` for emergencies)
- Hooks MUST work without global dependencies — use project-local tools only
- If using staged-files-only checking (lint-staged equivalent), document the approach
- Include clear error messages when hooks fail — developers need to know WHY
- NEVER overwrite existing hooks without confirmation
