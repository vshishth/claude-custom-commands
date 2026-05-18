---
description: Set up recurring automated tasks (dep checks, security scans, health checks)
argument-hint: task and interval (e.g., "security scan daily", "deps check weekly", "healthcheck every 6h")
allowed-tools: Read, Grep, Glob, Bash(crontab:*, find:*, cat:*, ls:*)
---

# Scheduled Automation

Act as a Principal Engineer setting up recurring automated tasks. Configure periodic checks that surface issues before they become incidents.

Current scheduled tasks:
!`crontab -l 2>/dev/null | head -10`

```
$ARGUMENTS
```

## Process

1. **Define the task** — Clarify what should run, how often, and what action to take on failure (notify, create issue, auto-fix).
2. **Select mechanism** — Choose the appropriate scheduling mechanism: CronCreate (Claude Code native), crontab (system), GitHub Actions schedule, or CI pipeline.
3. **Configure the schedule** — Set up the recurring task with appropriate interval, timeout, and failure handling.
4. **Define notifications** — Specify what happens when the task finds issues: log, notify, create ticket, or auto-remediate.
5. **Document** — Produce a summary of all scheduled tasks with their purpose and frequency.

## Recommended Recurring Tasks

| Task | Recommended Interval | Purpose |
|------|---------------------|---------|
| Security scan | Daily | Catch new CVEs in dependencies |
| Dependency freshness | Weekly | Flag outdated packages before they become debt |
| License compliance | Weekly | Catch new copyleft additions |
| Health check | Every 6 hours | Verify service availability |
| Secret rotation audit | Monthly | Flag secrets approaching rotation deadline |
| Config drift check | Daily | Catch environment inconsistencies |

## When Information is Insufficient

If the interval is unclear, recommend the standard interval from the table above. If the notification mechanism is unclear, default to stdout/log. If the task scope is too broad, ask what specifically to check.

## Output

### Scheduled Task
- **What:** [description]
- **When:** [cron expression + human-readable]
- **Timeout:** [max duration]
- **On failure:** [action]

### Setup Commands
```bash
# Commands to configure the schedule
```

### Monitoring
How to verify the scheduled task is running and check its history

## Constraints

- NEVER schedule tasks that modify production state without explicit confirmation
- All scheduled tasks MUST have a timeout — prevent runaway processes
- Include a way to run the task manually (for debugging)
- Scheduled tasks MUST be idempotent — safe to run multiple times
- Log all scheduled task executions for auditability
- NEVER schedule more frequently than the task takes to run (avoid overlap)
