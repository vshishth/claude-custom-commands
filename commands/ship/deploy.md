---
description: Design deployment strategy with rollback capabilities
argument-hint: application type, environment, and availability requirements
allowed-tools: Read, Glob
---

# Deployment Strategy

Design a deployment strategy for:

```
$ARGUMENTS
```

## Analysis

1. **Assess** the application's downtime tolerance, state management, and database migration needs
2. **Select strategy** - Blue/green, canary, rolling, or feature flags - justify the choice
3. **Design rollback** - How to revert quickly, including database rollback if applicable
4. **Define health checks** - What signals confirm a healthy deployment vs what triggers auto-rollback

## Output

- **Strategy**: Which approach and why
- **Deployment steps**: Ordered sequence with verification gates
- **Rollback procedure**: Step-by-step, including data considerations
- **Monitoring**: What to watch during and after deploy
- **Runbook**: Operational checklist for the deploy engineer
