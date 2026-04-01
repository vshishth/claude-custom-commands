---
description: Generate release notes from git history or change descriptions
argument-hint: version number, date range, or list of changes
allowed-tools: Bash(git log:*, git tag:*, git diff:*)
---

# Release Notes

Generate release notes based on:

```
$ARGUMENTS
```

Recent commits:
!`git log --pretty=format:"%h %s (%an)" -n 30 --no-merges 2>/dev/null || echo "No git history available"`

## Structure

### [Version] - [Date]

**Breaking Changes** - List any breaking changes with migration instructions

**New Features** - Grouped by area/component

**Improvements** - Performance, UX, and quality improvements

**Bug Fixes** - Grouped by severity

**Security** - Security patches with CVE references if applicable

**Deprecations** - What's deprecated and what to use instead

## Principles

- Write for the user, not the developer - explain impact, not implementation
- Lead with breaking changes so upgraders see them first
- Link to relevant issues/PRs for details
- Keep descriptions to one line each - link to docs for details
