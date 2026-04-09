---
description: Commit staged changes, create a branch, push, and open a draft pull request
argument-hint: optional description of changes
allowed-tools: Bash(git:*), mcp__github__create_pull_request, mcp__github__list_pull_requests
---

# Draft Pull Request

Act as a Principal Engineer. Create a clean draft PR from staged changes.

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
2. **Warn** if there are unstaged changes beyond what is staged — these will NOT be in the PR. Inform the user.
3. **Commit** staged changes only with a clean, conventional commit message (imperative mood, under 50 chars summary).
4. **Create a branch** from the current branch if on the default branch. Follow the project's branch naming convention (e.g., `feat/short-description`, `fix/short-description`). If already on a non-default feature branch, stay on it.
5. **Push** the branch to origin.
6. **Open a draft pull request** against the default branch using the GitHub MCP tool. If a PR template exists at `.github/PULL_REQUEST_TEMPLATE.md`, follow its structure. The PR title should match the commit summary. Include a clear description of what changed and why.
7. **Report** the PR URL when done.

## When Information is Insufficient

If on the default branch with no description provided, generate the branch name and PR description from the staged diff. If the remote is not configured, report the error and stop.

$ARGUMENTS

## Constraints

- NEVER force-push — if the branch has diverged, report the situation and ask for guidance
- NEVER reference Claude, AI, or any tool in commit messages or PR descriptions — write as a human engineer
- PR description must describe WHAT and WHY, never HOW
- Do not push to main/master directly
