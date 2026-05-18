---
description: Guided rollback procedure based on deployment type and current state
argument-hint: what to rollback (e.g., "last deploy", "migration 0042", "config change")
allowed-tools: Read, Grep, Glob, Bash(git log:*, git diff:*, git tag:*, helm history:*, kubectl get:*, find:*, grep:*)
---

# Rollback Guide

Act as a Principal Engineer executing a rollback. Produce a safe, step-by-step rollback procedure specific to this service's deployment method.

Deploy method:
!`ls helmfile.yaml docker-compose*.yml .github/workflows/ Makefile deploy/ 2>/dev/null`

Recent deploys:
!`git log --oneline --decorate -10 2>/dev/null`

```
$ARGUMENTS
```

## Process

1. **Identify rollback type** — Determine what needs rolling back: application code, database migration, configuration change, infrastructure change.
2. **Assess reversibility** — Flag irreversible changes (destructive migrations, deleted data, sent notifications). For irreversible items, propose forward-fix alternatives.
3. **Generate procedure** — Produce step-by-step rollback commands based on the detected deploy method (helm rollback, git revert + redeploy, terraform apply with previous state).
4. **Define verification** — After each rollback step, specify how to verify success (health checks, smoke tests, metric recovery).
5. **Document risks** — List what could go wrong during rollback and how to handle each failure mode.

## When Information is Insufficient

If the deployment method is unclear, ask. If the rollback target is ambiguous, show recent changes and ask which to revert. If database migrations are involved, check if they have down migrations before recommending rollback.

## Output

### Rollback Type: [code | migration | config | infra]
### Risk Level: [low | medium | high]
### Irreversible Components: [list or "none"]

### Procedure
1. [Pre-check] — Verify: [command]
2. [Rollback step] — `command`
   - Verify: [how to confirm]
3. [Post-rollback validation]

### If Rollback Fails
- Symptom → Recovery action

### Post-Rollback
- [ ] Verify health endpoints
- [ ] Check error rate metrics
- [ ] Notify stakeholders
- [ ] Create follow-up ticket for root cause

## Constraints

- NEVER rollback a database migration without verifying the down migration exists and is tested
- ALWAYS check for data written AFTER the bad deploy — rollback may lose recent writes
- Include a "point of no return" warning for irreversible steps
- Estimate time for each step
- If rollback requires downtime, state this explicitly upfront
