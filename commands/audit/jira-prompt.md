---
description: Review a Jira ticket's description and prompt for completeness, then suggest updates
argument-hint: JIRA-KEY (e.g., RSRV-3762) and optional Code: /path/to/source
allowed-tools: Read, Grep, Glob, Bash(git log:*, git blame:*, git diff:*), mcp__atlassian__getJiraIssue, mcp__atlassian__editJiraIssue, mcp__atlassian__addCommentToJiraIssue, mcp__atlassian__getConfluencePage, mcp__atlassian__searchJiraIssuesUsingJql
---

# Jira Prompt Audit

Act as a Principal Engineer. Review the given Jira ticket's description and prompt for clarity, completeness, and implementation-readiness. Identify gaps, suggest answers to open questions, and propose updates.

```
$ARGUMENTS
```

## Process

1. **Fetch the ticket** — Retrieve the Jira issue using the provided key. Read the description, comments, and linked issues for full context.
2. **Assess completeness** — Evaluate the ticket against these criteria:
   - Is the problem clearly stated with root cause identified?
   - Are reproduction steps accurate and complete?
   - Is the scope well-defined (what's in, what's out)?
   - Are file paths, line numbers, and code references included?
   - Is there a reference to existing patterns/conventions to follow?
   - Are acceptance criteria concrete and testable?
   - Are required dependencies or imports mentioned?
   - Could an AI coding tool implement this without follow-up questions?
3. **Investigate the code** (if a code path is provided) — Search the codebase to verify claims, find the root cause, identify existing patterns, and fill knowledge gaps.
4. **Identify open questions** — List any decisions that need to be made (scope, approach, wording, etc.) and suggest answers with rationale.
5. **Draft updates** — Prepare a revised description and/or comment that addresses all gaps.
6. **Present for review** — Show the proposed changes to the user. Do NOT apply any changes until explicitly approved.

## Output

Present findings in this structure:

- **Verdict**: Is the ticket implementation-ready? (Ready / Needs Updates / Incomplete)
- **Gaps found**: Bulleted list of what's missing or unclear
- **Open questions & suggested answers**: Table with Question | Suggested Answer | Rationale
- **Proposed description update**: The full revised description (if changes needed)
- **Proposed comment**: Investigation findings, answered questions, and implementation notes (cc: @Reserve Bot)

## Applying Changes (Requires Approval)

After presenting the proposed updates:
1. Ask the user to review and approve each change (description update, comment)
2. Only apply approved changes via the Atlassian MCP tools
3. Always include "cc: @Reserve Bot" in comments
4. Report what was applied and link to the ticket

## When Information is Insufficient

- If no Jira key is provided, ask for it
- If the ticket references code but no code path is given, ask for the repository/directory path
- If the ticket is too vague to assess (no steps to reproduce, no error description), flag this as "Incomplete" and suggest what information to gather before proceeding

## Constraints

- NEVER apply changes without explicit user approval — always present proposed updates first
- NEVER fabricate file paths or line numbers — only reference code you have verified exists
- NEVER remove information from the original ticket — only add or refine
- Always include "cc: @Reserve Bot" in comments added to the ticket
- Keep the description concise but implementation-ready — an AI coding tool should be able to implement from it without clarification
- Preserve the original reporter's reproduction steps unless they are factually wrong
- Use the project's established patterns as the basis for suggested fixes (grep for similar code)
