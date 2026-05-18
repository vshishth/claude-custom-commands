---
description: Generate incident response playbook with triage, communication, and post-mortem structure
argument-hint: incident description or alert name (e.g., "API 5xx spike", "database connection exhaustion")
allowed-tools: Read, Grep, Glob, Bash(grep:*, find:*, git log:*, git blame:*, curl:*)
---

# Incident Response

Act as a Principal Engineer leading incident response. Generate a structured playbook for triaging, mitigating, and resolving the described incident.

Service architecture:
!`find . -name "*.proto" -o -name "main.go" -o -name "index.ts" -o -name "docker-compose*.yml" | head -10 2>/dev/null`

Error handling patterns:
!`grep -rl "circuit.breaker\|retry\|timeout\|fallback\|healthz" --include="*.go" --include="*.ts" -l 2>/dev/null | head -10`

```
$ARGUMENTS
```

## Process

1. **Classify severity** — Based on the described symptoms, assign severity (SEV1-critical, SEV2-major, SEV3-minor) with reasoning.
2. **Identify blast radius** — Determine which users, services, and data flows are affected.
3. **Generate triage steps** — Produce immediate diagnostic steps: what to check, what logs to pull, what metrics to observe.
4. **Define mitigation options** — List fastest-to-implement mitigations: rollback, feature flag, traffic shift, manual intervention, scaling.
5. **Draft communication** — Generate stakeholder update template (who's affected, what we know, ETA, next update time).
6. **Outline post-mortem** — Structure the post-incident review: timeline, root cause, contributing factors, action items.

## When Information is Insufficient

If the incident is vague, ask for: what alerting triggered, which environment, when it started, what changed recently (deploys, config changes). If the service is unknown, analyze the current codebase for likely failure modes.

## Output

### Severity: SEV[1-3] — [one-line justification]

### Immediate Actions (first 5 minutes)
1. [Check/verify action]
2. [Mitigate action]

### Triage Checklist
- [ ] Check: [specific metric/log/endpoint]
- [ ] Verify: [dependency health]
- [ ] Confirm: [recent deploy/change]

### Mitigation Options (fastest first)
1. [Option] — ETA: [minutes], Risk: [low/med/high]

### Communication Template
> **Status:** Investigating | **Impact:** [scope] | **ETA:** [time]
> [2-sentence summary for stakeholders]

### Post-Mortem Structure
- Timeline, root cause, action items (template)

## Constraints

- Mitigation ALWAYS comes before root cause analysis — stop the bleeding first
- NEVER suggest "restart everything" without checking for data loss implications
- Communication must be jargon-free for non-technical stakeholders
- Every action item in post-mortem must have an owner placeholder and due date
- Include rollback as first mitigation option if a recent deploy correlates with the incident
