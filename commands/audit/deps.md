---
description: Analyze project dependencies for risks, bloat, and update needs
argument-hint: package.json, requirements.txt, go.mod, or similar
allowed-tools: Read, Grep, Glob, Bash(npm:*, pip:*, yarn:*, bundle:*, cargo:*, go:*, pnpm:*, npx:*)
---

# Dependency Analysis

Act as a Principal Engineer. Analyze dependencies for health, security, and bloat.

```
$ARGUMENTS
```

Current dependency tree:
!`npm list --depth=0 2>/dev/null || pip list 2>/dev/null || bundle list 2>/dev/null || cargo tree --depth=1 2>/dev/null || echo "Could not auto-detect dependencies"`

## Analysis

1. **Health check** — Outdated, deprecated, or unmaintained packages (no commits in >12 months)
2. **Security** — Known vulnerabilities (CVEs via `npm audit` / `pip audit` / equivalent), packages with poor security track records
3. **Bloat** — Unused dependencies, oversized packages, overlapping functionality
4. **Risk** — Single-maintainer packages, low adoption, missing types, license incompatibilities
5. **License compatibility** — Identify copyleft licenses (GPL, AGPL) that may conflict with the project's license. Flag missing license declarations.
6. **Transitive risks** — Check for risky transitive dependencies (deeply nested, unmaintained) not just direct dependencies
7. **Upgrades** — Breaking changes in available updates, migration effort required

## Output

- **Critical updates**: Security patches needed now (CVE ID, severity, affected version)
- **Recommended removals**: Unused or replaceable dependencies — every removal MUST include what to use instead
- **Upgrade plan**: Ordered list of updates with breaking change notes and migration effort
- **License matrix**: List of all dependency licenses with compatibility status
- **Alternatives**: Better packages to replace problematic ones (with justification)
- **SBOM recommendation**: If the project doesn't generate an SBOM (CycloneDX/SPDX), recommend adding it

## When Information is Insufficient

If the dependency file is not specified, auto-detect from project root. If multiple package managers are present, analyze all of them. If a package's maintenance status is unclear, check the repository's last commit date and open issue count.

## Constraints

- Every "remove this dependency" recommendation MUST include what to use instead (built-in, alternative package, or custom implementation)
- Security vulnerabilities with available patches are always top priority
- Do not modify any files — this is a read-only analysis
- Distinguish between direct and transitive dependency issues
