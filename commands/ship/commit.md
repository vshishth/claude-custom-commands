---
description: Create a well-structured git commit with conventional commit format
argument-hint: optional description of changes
allowed-tools: Bash(git:*)
---

# Git Commit

Act as a Principal Engineer. Create a clean, well-structured commit.

Current state:
!`git status --short`

Staged changes:
!`git diff --staged --stat`

Recent commits:
!`git log -5 --pretty=format:"%h %s" --no-merges`

## Process

1. **Check staged changes** — If nothing is staged, list unstaged files grouped by likely commit scope and ask the user what to stage. NEVER auto-stage all changes.
2. **Analyze the diff** — Read the staged diff to understand what changed and why.
3. **Assess scope** — If the staged diff exceeds 500 lines, suggest splitting into multiple commits by concern.
4. **Generate commit message** using conventional commit format:
   ```
   type(scope): summary (under 50 chars, imperative mood)

   body (WHAT changed and WHY, not HOW)

   Refs: #issue
   ```
   Types: feat, fix, refactor, perf, test, docs, build, ci, chore
5. **Execute** the commit.

## When Information is Insufficient

If there are no staged or unstaged changes, report "Nothing to commit — working tree is clean" and stop. If the purpose of changes is unclear from the diff alone, ask the user for context before writing the commit message.

$ARGUMENTS

## Constraints

- NEVER use `git add .` or `git add -A` — always require explicit user approval for what gets staged
- NEVER auto-stage all changes when nothing is staged — ask the user
- Do not mention Claude, AI, or any tool in commit messages
- If a `.pre-commit-config.yaml` or `.husky/` directory exists, note that pre-commit hooks will run
- Follow the project's existing commit message style if it differs from conventional commits
