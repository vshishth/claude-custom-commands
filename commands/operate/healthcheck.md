---
description: Verify service health across environments; check endpoints, deps, secrets
argument-hint: service name or directory (optional)
allowed-tools: Read, Grep, Glob, Bash(curl:*, aws ssm get-parameters-by-path:*, aws ssm get-parameter:*, chamber list:*, kubectl get:*, helm status:*, docker ps:*, grep:*)
---

# Service Health Check

Act as a Principal Engineer verifying production readiness. Systematically check all health dimensions for a service.

Project type:
!`ls go.mod package.json Cargo.toml requirements.txt docker-compose*.yml 2>/dev/null`

Deploy infrastructure:
!`ls -d deploy/ kubernetes/ helm/ helmfile.yaml .github/workflows/ Dockerfile 2>/dev/null`

```
$ARGUMENTS
```

## Process

1. **Identify endpoints** — Scan code for health endpoints (`/healthz`, `/readyz`, `/livez`, `/health`, `/status`). Report if none exist.
2. **Check dependencies** — Find external dependencies (databases, caches, queues, upstream services) from config/connection code. Verify connectivity if credentials are available.
3. **Verify secrets** — Discover required env vars from config loading code. If Chamber/SSM is detected, check which secrets exist vs. are missing.
4. **Validate deploy config** — Check Dockerfile, helm charts, or deploy manifests for misconfigurations (missing resource limits, no readiness probes, no graceful shutdown).
5. **Report health matrix** — Summarize findings in a structured table.

## When Information is Insufficient

If no service name is given, use the current directory. If no deploy configs exist, focus on code-level health (endpoints, dependency declarations, config loading). If AWS credentials are unavailable, skip live secret verification and report what SHOULD exist.

## Output

| Dimension | Status | Details |
|-----------|--------|---------|
| Health endpoints | pass/fail/missing | List found endpoints |
| Dependencies | pass/warn/fail | Connection status or config presence |
| Secrets | pass/warn/fail | Missing/present count |
| Deploy config | pass/warn/fail | Issues found |

Each failure MUST include the specific fix (file path + what to add/change).

## Constraints

- NEVER execute destructive commands or modify any files
- NEVER expose secret values in output — only report existence/absence
- If live checks fail, distinguish between "misconfigured" vs "credentials unavailable"
- Report missing health endpoints as a critical finding
