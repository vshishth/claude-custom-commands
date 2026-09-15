---
description: Start work on a Jira ticket — fetch it, create the branch, surface acceptance criteria and related memory, draft a PR-sized plan
argument-hint: JIRA-KEY (e.g. RSRV-4544) with optional short slug (e.g. RSRV-4544 name-only-takeout)
allowed-tools: Read, Grep, Glob, Bash(git status:*, git branch:*, git fetch:*, git checkout:*, git switch:*, git symbolic-ref:*, git log:*, git stash list:*, ls:*, cat:*), mcp__atlassian__getJiraIssue, mcp__atlassian__searchJiraIssuesUsingJql, mcp__github__list_pull_requests, mcp__github__search_issues
---

# Start Ticket

Set up everything needed to begin a ticket so the first hour is spent on the change, not on context gathering.

```
$ARGUMENTS
```

Current branch:
!`git branch --show-current`

Default branch:
!`git symbolic-ref refs/remotes/origin/HEAD --short 2>/dev/null`

Working tree:
!`git status --short`

Recent remote branches (for naming convention):
!`git branch -r --sort=-committerdate 2>/dev/null | grep -v HEAD | head -12`

Project memory index:
!`cat ~/.claude/projects/$(pwd | sed 's|/|-|g')/memory/MEMORY.md 2>/dev/null || echo "(no memory dir for this project)"`

## Process

1. **Parse the ticket key** from `$ARGUMENTS` (pattern `[A-Z][A-Z0-9]+-\d+`). If a slug follows the key, use it for the branch name; otherwise derive a 2–4 word kebab-case slug from the ticket summary.

2. **Fetch the ticket** with `getJiraIssue`. Extract: summary, description, acceptance criteria, issue type, priority, fix version, components, parent/epic, and linked issues. If the ticket has a parent epic, fetch it too — one level only.

3. **Check for existing work** before creating anything:
   - `git branch -a | grep -i <KEY>` — a local or remote branch may already exist. If so, offer to check it out instead of creating a new one.
   - `list_pull_requests` / `search_issues` for the key — an open PR may already exist. Report it.

4. **Create the branch** from an up-to-date default branch:
   - If the working tree is dirty, stop and ask whether to stash or commit first. Do not stash automatically.
   - `git fetch origin` then `git switch -c <branch> origin/<default>`.
   - **Match the repo's convention** from the remote branch list above, not a fixed rule. Observed patterns across SpotOn repos: `RSRV-4544-short-slug`, `feat/RSRV-4537-short-slug`, `cs-1976-short-slug`, `fix/short-slug`. Pick the dominant pattern in *this* repo. If no pattern is clear, use `<KEY>-<slug>`.

5. **Surface related memory.** Scan the memory index above for entries mentioning the ticket key, epic key, component, or touched module names. Read matching files and summarize the relevant gotchas in 1–3 lines each. Skip if nothing matches — do not pad.

6. **Draft the plan.** Restate the acceptance criteria as a checklist. Then propose a PR sequence: small, self-contained, ordered PRs (proto / migration / service / infra / docs are separate PRs when they'd otherwise be combined). For each PR: title, scope, and what must land before it. Note which AC each PR satisfies.

7. **Identify open questions** — anything in the ticket that is ambiguous, contradicts the codebase, or has no AC. Do not start implementing; that is `/build/implement`.

## When Information is Insufficient

- If `$ARGUMENTS` has no ticket key, ask for one. Do not guess from the branch name.
- If the ticket has no acceptance criteria, say so explicitly and derive a provisional checklist from the description, marked as *inferred*.
- If the repo has no remote branches to infer convention from, ask which pattern to use.
- If the ticket is not in a workable status (e.g. Done, Blocked), report the status and ask before proceeding.

## Output

- **Ticket**: `KEY — summary` · type · priority · fix version · epic (if any)
- **Branch**: name created (or existing branch checked out, or existing PR found)
- **Acceptance criteria**: checklist, marked *inferred* where applicable
- **Related memory**: bullets, or "none"
- **PR plan**: ordered list with scope and dependencies
- **Open questions**: bullets, or "none"

## Constraints

- Create the branch only. Do NOT implement, commit, or push.
- Do NOT transition the Jira ticket or comment on it — that's a human decision.
- Do NOT stash or discard working-tree changes without confirmation.
- Never reference Claude, AI, or tooling in the branch name.
- Honor the repo's observed branch convention over any default in this file.
