---
description: Automated dependency updates with compatibility analysis and PR creation
argument-hint: scope (e.g., "all", "security-only", "major", specific package name)
allowed-tools: Read, Grep, Glob, Bash(go list:*, go get:*, npm outdated:*, npm update:*, npm audit:*, npx:*, cargo:*, pip:*, git:*), mcp__github__create_pull_request
---

# Dependency Update

Act as a Principal Engineer managing dependency health. Analyze outdated dependencies, assess risk, and produce safe update batches.

Package manager:
!`ls go.mod go.sum package.json package-lock.json yarn.lock pnpm-lock.yaml Cargo.toml requirements.txt 2>/dev/null`

Current outdated:
!`(go list -m -u all 2>/dev/null | grep '\[' | head -20) || (npm outdated 2>/dev/null | head -20) || echo "run manually"`

```
$ARGUMENTS
```

## Process

1. **Inventory outdated** — List all dependencies with available updates. Categorize: patch (safe), minor (likely safe), major (breaking changes possible).
2. **Assess risk** — For each update, check: changelog for breaking changes, CVE fixes, deprecation notices. Flag high-risk updates.
3. **Group into batches** — Create update batches: security fixes first, then patches, then minor, then major. Each batch should be independently deployable.
4. **Apply updates** — Execute the update for the selected scope. Run tests to verify compatibility.
5. **Report results** — Show what was updated, test results, and any remaining issues.

## When Information is Insufficient

If scope is "all", recommend starting with security-only and patches. If tests fail after an update, identify the specific incompatibility and suggest the fix or a version pin. If the user wants a PR, create one per batch.

## Output

### Update Plan
| Package | Current | Latest | Type | Risk | CVEs Fixed |
|---------|---------|--------|------|------|-----------|

### Batch 1: Security Fixes (apply first)
### Batch 2: Patch Updates (safe)
### Batch 3: Minor Updates (review changelogs)
### Batch 4: Major Updates (breaking — requires code changes)

### Test Results After Update
- pass/fail with details on failures

## Constraints

- NEVER update all dependencies in a single commit — batch by risk level
- Security fixes MUST be prioritized over feature updates
- ALWAYS run tests after updates — never assume compatibility
- Pin exact versions for production dependencies (no ^ or ~ in critical paths)
- If a major update requires code changes, list the specific changes needed
- Create separate PRs for each batch to make rollback granular
