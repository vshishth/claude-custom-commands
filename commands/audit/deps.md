---
description: Analyze project dependencies for risks, bloat, and update needs
argument-hint: package.json, requirements.txt, go.mod, or similar
allowed-tools: Read, Grep, Glob, Bash(npm:*, pip:*, yarn:*, bundle:*, cargo:*, go:*)
---

# Dependency Analysis

Analyze dependencies for this project:

```
$ARGUMENTS
```

Current dependency tree:
!`npm list --depth=0 2>/dev/null || pip list 2>/dev/null || bundle list 2>/dev/null || cargo tree --depth=1 2>/dev/null || echo "Could not auto-detect dependencies"`

## Analysis

1. **Health check** - Outdated, deprecated, or unmaintained packages
2. **Security** - Known vulnerabilities (CVEs), packages with poor security track records
3. **Bloat** - Unused dependencies, oversized packages, overlapping functionality
4. **Risk** - Single-maintainer packages, low adoption, missing types, license incompatibilities
5. **Upgrades** - Breaking changes in available updates, migration effort required

## Output

- **Critical updates**: Security patches needed now
- **Recommended removals**: Unused or replaceable dependencies
- **Upgrade plan**: Ordered list of updates with breaking change notes
- **Alternatives**: Better packages to replace problematic ones
