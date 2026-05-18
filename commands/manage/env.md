---
description: Audit, diff, and sync environment variables across environments
argument-hint: environment name or action (e.g., "diff staging prod", "audit", "list")
allowed-tools: Read, Grep, Glob, Bash(aws ssm get-parameters-by-path:*, chamber list:*, chamber read:*, env:*, grep:*, find:*, diff:*, sort:*)
---

# Environment Management

Act as a Principal Engineer auditing environment configuration. Ensure parity between environments and catch misconfigurations before they cause incidents.

Config loading:
!`grep -rl "os.Getenv\|process.env\|viper\|envconfig\|env.Parse" --include="*.go" --include="*.ts" --include="*.js" 2>/dev/null | head -10`

Environment files:
!`find . -name ".env*" -o -name "*.env" -o -name "docker-compose*.yml" | head -10 2>/dev/null`

```
$ARGUMENTS
```

## Process

1. **Discover required vars** — Scan code for all environment variable reads. Build the complete list of required configuration.
2. **Categorize** — Group by: required (app crashes without it), optional (has default), secret (should be in SSM/vault, not plain env).
3. **Check sources** — If Chamber/SSM is used, list what's available per environment. If `.env` files exist, parse them.
4. **Diff environments** — Compare variable sets between environments. Flag: present in staging but missing in prod, different values that shouldn't differ, secrets in plaintext that should be in SSM.
5. **Report gaps** — Produce actionable report of misconfigurations.

## When Information is Insufficient

If no environment is specified, audit the current project's configuration requirements. If AWS credentials are unavailable, analyze code and local config files only, noting what you CANNOT verify remotely.

## Output

### Required Variables
| Variable | Source | Staging | Production | Status |
|----------|--------|---------|------------|--------|

### Issues Found
- Missing in production: `VAR_NAME` — Fix: `chamber write <service>/production VAR_NAME <value>`
- Plaintext secret: `DB_PASSWORD` in `.env` — Fix: move to Chamber
- Drift: `API_URL` differs unexpectedly between staging/prod

### Recommendations
Prioritized list of configuration fixes

## Constraints

- NEVER output actual secret values — only report existence/absence
- NEVER modify environment variables without explicit confirmation
- Distinguish between "missing" (will crash) and "different" (might be intentional)
- Flag any variable that looks like a secret (contains PASSWORD, KEY, TOKEN, SECRET) in plaintext files
