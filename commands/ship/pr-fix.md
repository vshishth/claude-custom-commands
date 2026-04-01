---
description: Review and resolve open PR comments with principal-engineer-level fixes
argument-hint: PR number or GitHub PR URL
allowed-tools: Read, Grep, Glob, Bash(git remote:*), mcp__github__get_pull_request, mcp__github__get_pull_request_comments, mcp__github__get_pull_request_reviews, mcp__github__get_pull_request_files
---

# PR Comment Resolver

Resolve all open review comments on a pull request. Act as a Principal Engineer.

**Input**: `$ARGUMENTS`

Current repo remote:
!`git remote get-url origin 2>/dev/null`

## Process

1. **Parse input** - Extract owner, repo, and PR number from the argument. If a bare number is given, infer owner/repo from the git remote above.
2. **Fetch context** - Use the GitHub MCP tools to retrieve:
   - PR details (title, description, base/head branches)
   - All review comments (inline code comments)
   - All reviews (top-level review bodies)
   - Changed files list
3. **Identify unresolved comments** - Focus on comments that are unresolved, requesting changes, or asking questions. Ignore resolved threads, approvals, and bot comments.
4. **Read source files** - For each unresolved comment, read the relevant file at the referenced line range plus surrounding context (~50 lines) to fully understand the code.
5. **Analyze and fix** - For each comment, provide a concrete resolution.

## Output Format

For each unresolved comment, output:

### Comment #N — @reviewer on `file:line`
> Original comment text (quoted)

**Analysis**: Why the reviewer raised this and whether they are correct.
**Fix**: The exact code change to resolve it, as a fenced diff block.
**Trade-offs**: Any alternative approaches considered, if relevant.

---

After all comments, output:

## Summary
- **Total comments**: N
- **Unresolved**: N
- **Fixes provided**: N
- **Items needing discussion**: N (list which ones and why)

## Principles

- Read-only. Do NOT commit, push, or modify the PR in any way.
- Be direct. If a reviewer is wrong, say so with reasoning.
- Prefer minimal, surgical fixes over large rewrites.
- Respect project conventions found in the codebase.
