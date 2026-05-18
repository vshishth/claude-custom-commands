---
description: Configuration drift detection between environments and repos
argument-hint: what to compare (e.g., "staging vs prod", "local vs deployed", "this repo vs template")
allowed-tools: Read, Grep, Glob, Bash(diff:*, grep:*, find:*, aws ssm get-parameters-by-path:*, kubectl get:*, cat:*, ls:*)
---

# Configuration Drift Detection

Act as a Principal Engineer auditing configuration consistency. Detect drift between environments, repos, or expected state and actual state.

Config files:
!`find . -name "*.yaml" -o -name "*.yml" -o -name "*.json" -o -name "*.toml" | grep -v node_modules | grep -i "config\|setting\|env\|deploy\|helm" | head -15 2>/dev/null`

Environment markers:
!`find . -path "*staging*" -o -path "*production*" -o -path "*dev*" | grep -v node_modules | head -10 2>/dev/null`

```
$ARGUMENTS
```

## Process

1. **Identify config surfaces** — Find all configuration: app config files, helm values, terraform variables, environment-specific overrides, feature flags.
2. **Establish expected baseline** — Determine what the "source of truth" is (template, staging, or a reference environment).
3. **Compare environments** — Diff configuration between the specified environments. Categorize differences: intentional (env-specific), drift (should match but doesn't), missing (exists in one but not another).
4. **Assess risk** — For each drift item, determine impact: could it cause an outage? Data loss? Security issue? Silent bug?
5. **Produce remediation** — For each unintentional drift, specify the exact fix (which file, which value, which command).

## When Information is Insufficient

If environments aren't specified, compare all detected environment configs against each other. If remote config can't be accessed (no credentials), analyze local config files only and report what should be verified remotely.

## Output

### Configuration Surfaces Analyzed
| Surface | Location | Environments |
|---------|----------|-------------|

### Drift Report
| Config Key | Expected | Actual (env) | Risk | Fix |
|-----------|----------|-------------|------|-----|

### Summary
- Intentional differences: [count]
- Drift (needs fixing): [count]
- Missing in [env]: [count]

### Remediation Commands
```bash
# Exact commands to fix each drift item
```

## Constraints

- NEVER assume differences are drift — many are intentional (different DB hosts per env is normal)
- Flag security-sensitive drift as critical (different auth settings, relaxed CORS, debug modes)
- Check for values that should NEVER match across environments (secrets, endpoints that should point to different hosts)
- Report config that exists in prod but not staging as a testing risk
- Include timestamp of when the analysis was performed
