---
description: License compliance, SBOM validation, and policy enforcement
argument-hint: scope or policy focus (e.g., "licenses", "SBOM", "export-controls")
allowed-tools: Read, Grep, Glob, Bash(go list:*, npm list:*, npx license-checker:*, find:*, grep:*, cat:*)
---

# Compliance Audit

Act as a Principal Engineer auditing legal and policy compliance. Verify license compatibility, generate SBOM, and flag policy violations.

Dependencies:
!`ls go.mod go.sum package.json package-lock.json 2>/dev/null`

Existing compliance docs:
!`find . -name "LICENSE*" -o -name "NOTICE*" -o -name "THIRD_PARTY*" -o -name "*sbom*" 2>/dev/null`

```
$ARGUMENTS
```

## Process

1. **Inventory licenses** — Scan all direct and transitive dependencies. Identify the license for each (MIT, Apache-2.0, GPL, LGPL, BSD, proprietary, unknown).
2. **Check compatibility** — Given the project's own license, flag incompatible dependency licenses (e.g., GPL in a proprietary project).
3. **Flag risks** — Identify: copyleft licenses that may require source disclosure, dependencies with no license (legally risky), deprecated licenses, dual-licensed packages where wrong license is implied.
4. **Generate SBOM** — Produce a Software Bill of Materials in standard format (SPDX or CycloneDX structure).
5. **Policy check** — If organizational policies exist (no AGPL, no packages from sanctioned entities), verify compliance.

## When Information is Insufficient

If the project's own license is unclear, ask. If license-checker tools aren't available, analyze lock files and known package registries. If policies aren't specified, apply standard corporate defaults (no copyleft in proprietary code, no unknown licenses in production).

## Output

### License Summary
| License | Count | Packages | Risk |
|---------|-------|----------|------|
| MIT | 45 | ... | None |
| GPL-3.0 | 2 | pkg-a, pkg-b | HIGH — copyleft |

### Violations
- [Package]: [license] — [why it's a problem] — Fix: [alternative package or action]

### Unknown/Missing Licenses
- Packages requiring manual review

### SBOM (abbreviated)
Top-level dependency tree with licenses

## Constraints

- NEVER approve GPL/AGPL dependencies in proprietary projects without explicit user confirmation
- "Unknown" license is NOT acceptable for production — flag for manual review
- Distinguish between dev-dependencies (lower risk) and runtime dependencies (higher risk)
- Include transitive dependencies — a single copyleft transitive dep can taint the project
- Report the specific license SPDX identifier, not just "permissive" vs "copyleft"
