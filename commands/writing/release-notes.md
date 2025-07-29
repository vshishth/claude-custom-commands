---
description: Generate structured release notes from git history or change descriptions
argument-hint: git log information or list of changes
allowed-tools: Bash(git log:*)
---

# Release Notes Generator

## Context

Recent changes for inclusion in release notes:
!`git log --pretty=format:"%h - %s (%an, %ar)" -n 20 2>/dev/null || echo "No git history available"`

## Instructions

I'll generate comprehensive release notes based on the provided information:

```
$ARGUMENTS
```

## Release Structure

### Release Overview
- Release version
- Release date
- Release theme/focus
- Compatibility considerations
- Upgrade recommendations

### What's New
[Features grouped by component or area]
- Major new features with brief descriptions
- UI/UX improvements
- Performance enhancements
- New APIs or integration points

### Improvements & Enhancements
[Organized by component or functional area]
- Usability improvements
- Performance optimizations
- Minor feature enhancements
- Documentation updates

### Bug Fixes
[Grouped by severity or component]
- Critical bug fixes
- Security issue resolutions
- Stability improvements
- Edge case handling

### Breaking Changes
[If applicable]
- API changes
- Behavioral differences
- Configuration changes
- Migration instructions

### Deprecations
[If applicable]
- Deprecated features
- Sunset timeline
- Migration paths
- Alternative approaches

### Known Issues
- Outstanding bugs
- Workarounds for known problems
- Planned fixes

### Security Updates
- Security vulnerabilities addressed
- CVE references
- Recommended actions

## Additional Information
- Contributors
- Documentation links
- Support channels
- Feedback mechanisms