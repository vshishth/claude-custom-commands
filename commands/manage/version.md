---
description: Semantic versioning — bump, changelog generation, and tag management
argument-hint: bump type or version (e.g., "patch", "minor", "major", "1.5.0")
allowed-tools: Read, Grep, Glob, Bash(git tag:*, git log:*, git diff:*, npm version:*, cat:*, find:*)
---

# Version Management

Act as a Principal Engineer managing releases. Determine the appropriate version bump, generate changelog entries, and create the version tag.

Current version:
!`git describe --tags --abbrev=0 2>/dev/null || echo "no tags"`

Recent changes since last tag:
!`git log $(git describe --tags --abbrev=0 2>/dev/null)..HEAD --oneline --no-merges 2>/dev/null | head -20`

Version files:
!`find . -name "version.go" -o -name "VERSION" -o -name "package.json" | head -5 2>/dev/null`

```
$ARGUMENTS
```

## Process

1. **Determine current version** — Find the latest tag or version file. If no versioning exists, recommend starting at 0.1.0.
2. **Analyze changes** — Categorize commits since last release using conventional commit prefixes: feat (minor), fix (patch), breaking change (major).
3. **Calculate bump** — If bump type isn't specified, recommend based on commit analysis. If specified, validate it makes sense given the changes.
4. **Generate changelog** — Group changes by category (Features, Fixes, Breaking Changes, Other). Include commit references.
5. **Apply version** — Update version in relevant files (package.json, version.go, VERSION), create git tag.

## When Information is Insufficient

If no conventional commits are used, classify changes by file path and diff size. If the bump type conflicts with the changes (e.g., "patch" requested but breaking changes exist), warn and ask for confirmation.

## Output

### Version: [old] → [new]
### Bump Type: [patch|minor|major] — [justification]

### Changelog
#### Features
- feat: description (commit-hash)
#### Fixes
- fix: description (commit-hash)
#### Breaking Changes
- BREAKING: description (commit-hash)

### Commands to Execute
```bash
git tag -a v1.2.3 -m "Release v1.2.3"
git push origin v1.2.3
```

## Constraints

- NEVER create a major version bump without explicit confirmation from the user
- NEVER tag without ensuring all tests pass on the current commit
- Changelog MUST include all commits since last tag — don't silently skip any
- If breaking changes exist and bump type is not "major", WARN the user explicitly
- Version format MUST follow semver (vX.Y.Z) unless the project uses a different convention
- Do not push tags automatically — provide the command for the user to execute
