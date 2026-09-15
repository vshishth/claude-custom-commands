---
description: Commit staged changes, push, open a draft PR titled with the branch's Jira key, and report CI status
argument-hint: optional description of changes, or "ready" to open as non-draft
allowed-tools: Read, Bash(git status:*, git diff:*, git branch:*, git symbolic-ref:*, git log:*, git add:*, git commit:*, git push:*, git fetch:*, git rev-list:*, git switch:*, git remote:*, cat:*, ls:*), mcp__github__create_pull_request, mcp__github__list_pull_requests, mcp__github__get_pull_request, mcp__github__get_pull_request_status, mcp__teamcity
---

# Draft Pull Request

Turn staged changes into a small, reviewable draft PR that links to its Jira ticket and has a known CI status before you hand it off.

```
$ARGUMENTS
```

Current branch:
!`git branch --show-current`

Default branch:
!`git symbolic-ref refs/remotes/origin/HEAD --short 2>/dev/null`

Working tree:
!`git status --short`

Staged changes:
!`git diff --staged --stat`

Commits ahead of default:
!`git log --oneline origin/$(git symbolic-ref refs/remotes/origin/HEAD --short 2>/dev/null | sed 's|origin/||')..HEAD 2>/dev/null | head -20`

Recent commit style:
!`git log -8 --pretty=format:"%s" --no-merges`

PR template:
!`cat .github/PULL_REQUEST_TEMPLATE.md .github/pull_request_template.md 2>/dev/null | head -60`

## Process

1. **Preflight**
   - If on the default branch, stop. Run `/ship/start <KEY>` first, or ask for a branch name. Never commit to main/master/develop.
   - If nothing is staged **and** no commits are ahead of default, list unstaged files and ask what to stage. Do not `git add -A`.
   - If there are unstaged or untracked changes, warn that they will NOT be in the PR. Continue.
   - Check `list_pull_requests` for an open PR on this branch. If one exists, skip to step 5 (push + report) instead of creating a duplicate.

2. **Derive the Jira key** from the branch name (pattern `[A-Z][A-Z0-9]+-\d+`, case-insensitive — `cs-1976-...` → `CS-1976`). If none is found, proceed without one and say so.

3. **Size check.** Count files and lines in the staged diff plus commits ahead of default. If the change spans more than one concern (e.g. proto + service + infra, or migration + handler + docs), say so and propose a split into ordered PRs before committing. Ask whether to proceed as-is or split. A single PR should be reviewable in one sitting.

4. **Commit** (only if there are staged changes)
   - Match the repo's existing commit style from the log above. Default to conventional commits: `type(scope): summary`, imperative, ≤ 72 chars.
   - Body: what and why. No co-author trailers of any kind.

5. **Push** with `git push -u origin <branch>`. If the remote branch exists and has diverged, stop and report — do not force-push.

6. **Open the PR** via `create_pull_request` against the default branch.
   - Draft by default. Non-draft only if `$ARGUMENTS` contains `ready`.
   - Title: `<KEY>: <summary>` when a key exists (e.g. `RSRV-4544: Support name-only takeout orders`), otherwise the commit summary.
   - Body: follow the PR template if one exists. Otherwise: **What** · **Why** · **Testing** (what you ran, not what you intend to run) · **Jira** link `https://spoton.atlassian.net/browse/<KEY>`.
   - If this PR is one of a sequence, state its position and what it depends on.

7. **CI status.** Wait briefly, then check the PR's commit status via `get_pull_request_status`. If TeamCity is the CI, use the TeamCity tools to find the build for this branch and report state (queued / running / passed / failed). If failed, pull the failing step's log excerpt — do not attempt to fix in this command.

8. **Report**: PR URL · draft/ready · title · CI state · any warnings from steps 1–3.

## When Information is Insufficient

- No default branch detected: ask which branch to target.
- No remote configured: report and stop.
- No Jira key in the branch and `$ARGUMENTS` doesn't supply one: open the PR without a key, and say so in the report.
- PR template has required sections you cannot fill (e.g. screenshots, rollback plan): leave them with a `TODO:` marker and call them out in the report.

## Constraints

- NEVER force-push. NEVER push to the default branch.
- NEVER `git add -A` or stage files the user did not stage.
- NEVER reference Claude, AI, or tooling in commits, titles, or PR bodies. No co-author trailers.
- PR body describes WHAT and WHY. Reviewers read the diff for HOW.
- Do NOT fix CI failures here — report them. Use `/ship/pr-fix` or `/build/fix`.
- Do NOT transition or comment on the Jira ticket.
