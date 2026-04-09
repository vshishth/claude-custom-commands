---
description: Design deployment strategy with rollback capabilities
argument-hint: application type, environment, and availability requirements
allowed-tools: Read, Grep, Glob
---

# Deployment Strategy

Act as a Principal Engineer. Design a production deployment strategy with full rollback capability.

```
$ARGUMENTS
```

## Process

1. **Pre-deployment validation** — Define what must pass before deploy begins:
   - All tests green, no known critical issues
   - Database migrations backward-compatible with current app version
   - Feature flags configured for new functionality
   - Artifacts built, signed, and verified
2. **Assess risk profile** — Downtime tolerance, stateful vs stateless, database migration complexity, number of dependent services
3. **Select strategy** — Blue/green, canary, rolling, or feature-flag-based — justify based on the risk profile:
   - **Blue/green**: Best for zero-downtime with instant rollback (requires 2x infrastructure)
   - **Canary**: Best for high-traffic services where gradual exposure reduces blast radius
   - **Rolling**: Best for stateless services where partial deployment is safe
   - **Feature flags**: Best when code is already deployed but behavior needs gating
4. **Define traffic management** — For canary: specify percentages (1% → 5% → 25% → 100%), soak time at each stage, and success metrics to proceed
5. **Design rollback** — Automated triggers and manual procedure:
   - Auto-rollback triggers: error rate > X%, latency p99 > Yms, health check failures
   - Manual rollback: step-by-step procedure including database rollback if applicable
6. **Smoke tests** — Define minimum checks that must pass post-deploy (health endpoint, critical user flow, dependency connectivity)

## Output

- **Strategy**: Which approach and why
- **Pre-deployment checklist**: Ordered verification gates
- **Deployment steps**: Ordered sequence with success criteria at each stage
- **Rollback procedure**: Step-by-step with specific thresholds and data considerations
- **Smoke tests**: Minimum post-deploy verifications
- **Monitoring**: What to watch during and after deploy (metrics, logs, alerts)
- **Runbook**: Operational checklist for the deploy engineer

## When Information is Insufficient

If the application type is not specified, analyze the project structure to determine it. If availability requirements are unspecified, assume 99.9% uptime (8.76 hours/year downtime budget). If the deployment platform is unknown, design platform-agnostic steps.

## Constraints

- Every strategy MUST include a tested rollback procedure — no deploy without rollback
- Canary deployments MUST specify soak time and success criteria before proceeding to the next stage
- Database migrations MUST be backward-compatible with the currently-running app version
- Never deploy directly to production without a staging verification step
