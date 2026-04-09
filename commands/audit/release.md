---
description: Generate release notes from git history or change descriptions
argument-hint: version number, date range, or list of changes
allowed-tools: Bash(git log:*, git tag:*, git diff:*)
---

# Release Notes

Act as a Principal Engineer. Generate structured, user-facing release notes.

```
$ARGUMENTS
```

Recent commits:
!`git log --pretty=format:"%h %s (%an)" -n 30 --no-merges 2>/dev/null || echo "No git history available"`

## Process

1. **Detect previous release** — Find the most recent release tag. If no tags exist, use the beginning of git history.
2. **Collect changes** — Gather all commits between previous tag and HEAD (or specified range)
3. **Categorize** — Group commits by type using conventional commit prefixes if available, otherwise infer from commit content
4. **Suggest version** — If no version number is provided, suggest the next version based on changes: MAJOR for breaking changes, MINOR for features, PATCH for fixes only
5. **Generate** the release notes in the structure below

## Structure

### [Version] - [Date]

**Breaking Changes** — List any breaking changes with migration instructions

**New Features** — Grouped by area/component

**Improvements** — Performance, UX, and quality improvements

**Bug Fixes** — Grouped by severity

**Security** — Security patches with CVE references if applicable

**Deprecations** — What's deprecated and what to use instead

**Internal Notes** — Migration steps, infrastructure changes, or operational notes for the deploying team (mark as internal, not for end users)

## When Information is Insufficient

If no version number is provided, suggest one based on semantic versioning rules applied to the changes found. If the git history is empty or unavailable, ask the user for a list of changes.

## Constraints

- Write for the user, not the developer — explain impact, not implementation
- Lead with breaking changes so upgraders see them first
- Link to relevant issues/PRs for details
- Keep descriptions to one line each — link to docs for details
- Follow Keep a Changelog format (keepachangelog.com) unless the project has an established format
- If the project uses semantic versioning, verify the version bump matches the change types
