---
description: Generate or update operational runbooks from code and deploy configs
argument-hint: service name or operational scenario (e.g., "database failover", "deployment")
allowed-tools: Read, Grep, Glob, Bash(find:*, grep:*, git log:*, cat:*, ls:*)
---

# Runbook Generator

Act as a Principal Engineer codifying operational knowledge. Generate runbooks that enable any on-call engineer to handle scenarios without needing the original developer.

Deploy configuration:
!`find . -path "*/deploy/*" -o -name "helmfile.yaml" -o -name "docker-compose*.yml" -o -name "*.github/workflows/*" 2>/dev/null | head -10`

Health and monitoring:
!`grep -rl "healthz\|readyz\|metrics\|prometheus\|datadog\|alert" --include="*.go" --include="*.ts" --include="*.yaml" -l 2>/dev/null | head -10`

```
$ARGUMENTS
```

## Process

1. **Identify operational scenarios** — From code and config, determine the key operational scenarios: deployment, rollback, scaling, database operations, secret rotation, dependency failures.
2. **Extract procedures** — For each scenario, derive the step-by-step procedure from deploy scripts, CI configs, and infrastructure code.
3. **Add verification steps** — After each action step, include how to verify it worked (health checks, log queries, metric checks).
4. **Document escalation** — Include when to escalate, to whom, and what information to gather before escalating.
5. **Include recovery** — For failure scenarios, document the recovery procedure and what "healthy" looks like.

## When Information is Insufficient

If no specific scenario is requested, generate runbooks for the three most critical operations: deploy, rollback, and incident triage. If deploy tooling is unfamiliar, document what you can see and flag unknowns for the operator to fill in.

## Output

### Runbook: [Scenario Name]

**When to use:** [trigger condition]
**Estimated time:** [minutes]
**Required access:** [list of credentials/tools needed]

#### Steps
1. [Action] — `command to run`
   - Verify: [how to confirm success]
2. [Next action]...

#### If Something Goes Wrong
- Symptom → Recovery action

#### Escalation
- Escalate if: [condition]
- Contact: [team/channel]
- Provide: [information to gather]

## Constraints

- Every step MUST include a verification substep — never assume success
- Commands MUST be copy-pasteable (no placeholders without explanation)
- NEVER include secrets or credentials in runbooks — reference where to find them
- Include estimated time for each procedure
- Flag steps that are irreversible with explicit warnings
