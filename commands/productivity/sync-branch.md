---
description: Merge latest main/develop into current branch and resolve conflicts
argument-hint: optional base branch (defaults to main or develop)
allowed-tools: Read, Grep, Glob, Bash(git:*)
---

# Sync Branch

Current branch:
!`git branch --show-current`

Default branch:
!`git symbolic-ref refs/remotes/origin/HEAD --short 2>/dev/null`

Working tree status:
!`git status --short`

## Instructions

1. **Preflight checks**
   - If there are uncommitted changes, stash them with `git stash` before proceeding. Note this so you can pop them at the end.
   - Determine the base branch: use `$ARGUMENTS` if provided, otherwise use the default branch detected above (typically `main` or `develop`).

2. **Fetch and merge**
   - Run `git fetch origin` to get the latest remote state.
   - Run `git merge origin/<base-branch>` into the current branch.
   - If the merge completes cleanly, skip to step 5.

3. **Resolve conflicts** (if any)
   - List all conflicted files with `git diff --name-only --diff-filter=U`.
   - For each conflicted file:
     a. Read the file to see the conflict markers.
     b. Read the surrounding code and related files to understand project conventions.
     c. **Favor the base branch (main/develop) as the source of truth** — accept their changes unless the current branch's version is clearly correct and intentional.
     d. Edit the file to remove all conflict markers with the resolved content.
     e. Stage the resolved file with `git add`.

4. **Validate resolution**
   - Confirm no conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`) remain in any file.
   - Run the project's lint/build/test commands if a standard script is detected (e.g., `npm test`, `make test`, `cargo check`).

5. **Finalize**
   - If changes were stashed in step 1, run `git stash pop`.
   - Report what happened: files merged, conflicts resolved, and any test results.

## Principles

- Main/develop is the source of truth — when in doubt, prefer upstream changes.
- Preserve intentional feature-branch work; only override when it conflicts with upstream.
- Respect existing project structure, naming conventions, and code style.
- Do NOT push. The user decides when to push.
- Do NOT force-push or rebase — use merge to preserve history.
