---
description: Design observability setup — metrics, logs, traces, alerts, dashboards
argument-hint: service name or observability focus area (e.g., "latency", "error rates", "SLOs")
allowed-tools: Read, Grep, Glob, Bash(find:*, grep:*, cat:*, ls:*)
---

# Observability Design

Act as a Principal Engineer designing observability for a service. Produce a comprehensive monitoring strategy covering metrics, logs, traces, and alerts.

Current instrumentation:
!`grep -rl "prometheus\|datadog\|otel\|opentelemetry\|metrics\|statsd" --include="*.go" --include="*.ts" --include="*.yaml" -l 2>/dev/null | head -10`

Existing dashboards/alerts:
!`find . -path "*monitor*" -o -path "*alert*" -o -path "*dashboard*" -o -path "*grafana*" 2>/dev/null | head -10`

```
$ARGUMENTS
```

## Process

1. **Assess current state** — What's already instrumented? What's the telemetry stack (Prometheus, Datadog, OTel, CloudWatch)?
2. **Define SLIs** — Identify the Service Level Indicators that matter: latency (p50/p95/p99), error rate, throughput, saturation.
3. **Design metrics** — Specify custom metrics to add: name, type (counter/gauge/histogram), labels, and where in code to emit them.
4. **Design structured logging** — Define log levels, required fields, and correlation IDs for request tracing.
5. **Design alerts** — Specify alert rules: condition, threshold, window, severity, and runbook link.
6. **Propose dashboards** — Outline dashboard panels grouped by: golden signals, dependencies, business metrics.

## When Information is Insufficient

If no telemetry stack is detected, recommend OpenTelemetry as the vendor-neutral default. If the service type is unclear, design for a generic request-serving service and ask for refinement.

## Output

### SLIs & SLOs
| Signal | SLI | SLO Target | Current |
|--------|-----|-----------|---------|

### Metrics to Add
| Metric Name | Type | Labels | Location (file:line) |

### Alert Rules
| Alert | Condition | Severity | Runbook |
|-------|-----------|----------|---------|

### Dashboard Layout
- Panel descriptions grouped by category

### Implementation Steps
Prioritized list of instrumentation changes with file paths

## Constraints

- Use RED method for request-serving services (Rate, Errors, Duration)
- Use USE method for resources (Utilization, Saturation, Errors)
- Alerts MUST have runbook references — no alert without a response procedure
- Prefer histograms over summaries for latency (they're aggregatable)
- Every alert must have clear ownership and escalation path
