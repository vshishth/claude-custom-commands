---
description: Commit staged changes, create a branch, push, and open a draft pull request
argument-hint: optional description of changes
allowed-tools: Bash(git:*), mcp__github__create_pull_request, mcp__github__list_pull_requests
---

# Draft Pull Request

Current state:
!`git status --short`

Staged changes:
!`git diff --staged --stat`

Current branch:
!`git branch --show-current`

Default branch:
!`git symbolic-ref refs/remotes/origin/HEAD --short`

Recent commits:
!`git log -5 --pretty=format:"%h %s" --no-merges`

## Instructions

1. **Verify** there are staged changes. If nothing is staged, list unstaged files and ask what to stage — do not commit everything automatically.
2. **Commit** staged changes only with a clean, conventional commit message (imperative mood, under 50 chars summary). Do not mention Claude or AI in the commit message.
3. **Create a branch** from the current branch if not already on a feature branch. Follow the project's branch naming convention (e.g., `feat/short-description`, `fix/short-description`). If already on a non-default feature branch, stay on it.
4. **Push** the branch to origin.
5. **Open a draft pull request** against the default branch (main/develop) using the GitHub MCP tool. The PR title should match the commit summary. Include a clear description of what changed and why.
6. **Report** the PR URL when done.

Do not reference Claude, AI, or any tool in commit messages or PR descriptions. Write as a human engineer would.

$ARGUMENTS
