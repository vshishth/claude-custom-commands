---
description: Emergency hotfix workflow — branch from release, cherry-pick, fast-track PR
argument-hint: description of the fix or commit SHA to cherry-pick
allowed-tools: Read, Grep, Glob, Bash(git:*), mcp__github__create_pull_request, mcp__github__list_pull_requests, mcp__github__get_pull_request
---

# Hotfix

Act as a Principal Engineer executing an emergency hotfix. Speed matters, but correctness matters more — a bad hotfix is worse than the original bug.

Current state:
!`git status --short`

Current branch:
!`git branch --show-current`

Recent tags:
!`git tag --sort=-creatordate | head -5 2>/dev/null`

Release branches:
!`git branch -r | grep -i "release\|hotfix\|main\|master" | head -10 2>/dev/null`

```
$ARGUMENTS
```

## Process

1. **Identify the target** — Determine which release/production branch needs the fix. Use the most recent tag or release branch as the base.
2. **Create hotfix branch** — Branch from the production base: `hotfix/<short-description>` naming convention.
3. **Apply the fix** — Either cherry-pick the specified commit or implement the minimal fix described. Keep changes to the absolute minimum required.
4. **Verify** — Run tests scoped to the affected area. Confirm the fix addresses the issue without side effects.
5. **Open fast-track PR** — Create a PR marked as urgent/hotfix against the release branch. Include: what broke, root cause, fix applied, rollback plan.

## When Information is Insufficient

If no release branch or tag exists, ask which branch represents production. If the fix description is vague, ask for the specific error or behavior to fix. If cherry-pick has conflicts, resolve them and explain what was adjusted.

## Output

- Hotfix branch name and base
- Changes applied (files modified, lines changed)
- Test results for affected area
- PR URL with fast-track label

## Constraints

- NEVER include unrelated changes in a hotfix — scope is sacred
- NEVER force-push a hotfix branch
- ALWAYS include a rollback plan in the PR description
- Hotfix commits MUST use format: `fix: <description> [HOTFIX]`
- If tests fail after the fix, STOP and report — do not ship a broken hotfix
- Ask for confirmation before pushing if the fix touches more than 3 files
