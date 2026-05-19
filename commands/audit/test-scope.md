---
description: Analyze Jira tickets and PRs to generate comprehensive test scope and QA checklist
argument-hint: JIRA-KEY[,JIRA-KEY,...] (e.g., RSRV-4334 or RSRV-4334,RSRV-4335)
allowed-tools: Read, Grep, Glob, Bash(git log:*, git diff:*, git show:*, git blame:*, find:*), mcp__atlassian__getJiraIssue, mcp__atlassian__searchJiraIssuesUsingJql, mcp__github__get_pull_request, mcp__github__get_pull_request_files, mcp__github__get_file_contents, mcp__github__list_pull_requests, mcp__github__search_code, mcp__github__search_issues
---

# Test Scope Analysis

Act as a Principal QA Engineer and Staff Software Engineer. Given one or more Jira tickets, automatically discover all related PRs and code changes, then generate a comprehensive test scope analysis with actionable test cases.

```
$ARGUMENTS
```

## Process

1. **Fetch tickets** — Retrieve each Jira issue. Extract: summary, description, acceptance criteria, linked issues, fix versions, and components.

2. **Discover related PRs** — For each ticket key, search GitHub for PRs referencing it (by branch name pattern `TICKET-KEY/` or PR title/body containing the key). Fetch PR details and changed files for every related PR.

3. **Analyze code changes** — For each PR, examine the diff to understand:
   - Which modules/services/layers are touched (API, service, repository, UI, jobs, migrations)
   - Nature of changes (new feature, modification, deletion, refactor)
   - Data model changes (new columns, nullable changes, type changes, new tables)
   - API surface changes (new endpoints, changed request/response contracts, removed endpoints)
   - Configuration or environment changes
   - Security-sensitive changes (auth, permissions, token handling, input validation)
   - Background job / scheduled task changes
   - Cache invalidation changes
   - Third-party integration changes

4. **Map impact areas** — From the changed files, identify:
   - Direct impacts: features explicitly changed
   - Indirect impacts: features that consume changed APIs, models, or services
   - Shared utilities or base classes modified (high blast radius)
   - Database schema changes that affect other consumers

5. **Cross-reference test coverage** — Search for existing tests related to changed files:
   - Unit tests (look for `*Tests*`, `*Spec*`, `*test*` files matching changed modules)
   - Integration tests
   - Note which changed code paths have NO existing test coverage

6. **Assess risk** — Evaluate each change for:
   - Reversibility (can it be rolled back safely?)
   - Data migration risk (does it alter existing data or schema?)
   - Blast radius (how many features/users are affected?)
   - Edge cases (null handling, race conditions, backward compatibility)

## Output

Generate a structured report with these sections:

### 1. Change Summary
Table: Ticket | PR | Files Changed | Nature of Change

### 2. Impact Analysis
Group by impact area:
- **Database/Schema** — migrations, model changes, nullable changes
- **API Contracts** — new/changed/removed endpoints, request/response shape changes
- **Business Logic** — service layer changes, new rules, changed behavior
- **UI/UX** — view changes, new buttons, changed workflows
- **Background Jobs** — cron/nightly job changes, scheduling changes
- **Configuration/Environment** — env vars, feature flags, config changes
- **Security/Auth** — permission changes, auth flow changes
- **Integrations** — third-party API changes, webhook changes

### 3. Functional Test Cases
For each feature area, generate numbered test cases with:
- **ID**: TC-{area}-{number}
- **Scenario**: What to test
- **Steps**: Numbered steps to execute
- **Expected Result**: Specific observable outcome
- **Priority**: P0 (blocking) / P1 (high) / P2 (medium)

### 4. Regression Test Areas
Identify features NOT directly changed but at risk due to shared dependencies. For each:
- What could break
- How to verify it still works
- Priority of regression check

### 5. Risk Assessment
Table: Risk | Likelihood | Impact | Mitigation
Summarize overall release risk as: Low / Medium / High / Critical

### 6. Test Coverage Gaps
List changed code paths that have no corresponding automated tests. For each gap:
- What's untested
- Suggested test to add
- Whether manual testing can cover it in the interim

### 7. QA Checklist
A flat, copy-paste-ready checklist using `- [ ]` format, grouped by priority:
- P0 items first (must pass before release)
- P1 items (should pass, release-blocking bugs here are escalated)
- P2 items (nice to verify, won't block release)

## When Information is Insufficient

- If no Jira key is provided, ask for it
- If PRs cannot be found automatically, ask the user for PR numbers or branch names
- If the repository is ambiguous (multiple repos), ask which repo to search
- If acceptance criteria are missing from the ticket, note this as a gap and derive test cases from the code changes instead
- Default repository: `Seat-Ninja/Server` unless another is specified or discovered

## Constraints

- NEVER fabricate test cases for changes that don't exist — only generate tests for actual observed changes
- ALWAYS fetch and read the actual PR diffs — do not guess what changed from ticket description alone
- Cross-reference ticket acceptance criteria against generated test cases — flag any AC without a corresponding test case
- Flag any destructive database change (column removal, type narrowing) as P0 risk
- If a migration exists, always include a "migration rollback" test scenario
- Keep test case steps concrete and reproducible — no vague "verify it works" steps
- Include both happy path AND error/edge cases for each feature area
- For UI changes, include both functional and visual verification steps
