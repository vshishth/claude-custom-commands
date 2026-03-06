---
description: Create a well-structured git commit with conventional commit format
argument-hint: optional description of changes
allowed-tools: Bash(git:*)
---

# Git Commit

Current state:
!`git status --short`

Staged changes:
!`git diff --staged --stat`

Recent commits:
!`git log -5 --pretty=format:"%h %s" --no-merges`

## Instructions

1. **Analyze** the staged changes (or all changes if nothing is staged)
2. **Generate** a conventional commit message:
   ```
   type(scope): summary (under 50 chars, imperative mood)

   body (WHAT changed and WHY, not HOW)

   Refs: #issue
   ```
   Types: feat, fix, refactor, perf, test, docs, build, ci, chore
3. **Execute** the commit

If changes aren't staged, suggest what to stage and what to split into separate commits.

$ARGUMENTS
