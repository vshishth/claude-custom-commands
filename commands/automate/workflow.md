---
description: Create compound multi-step workflows that chain commands with quality gates
argument-hint: workflow name or description (e.g., "implement-and-ship", "audit-sweep", custom description)
allowed-tools: Read, Grep, Glob, Bash(find:*, cat:*, ls:*)
---

# Workflow Orchestration

Act as a Principal Engineer designing compound workflows. Chain multiple commands with quality gates between steps, ensuring each stage passes before proceeding.

Available commands:
!`find ~/.claude/commands/commands -name "*.md" | sed 's|.*/commands/commands/||;s|\.md$||;s|/|:|' | sort`

```
$ARGUMENTS
```

## Process

1. **Define the workflow** — Based on the description, select the appropriate command sequence. If a predefined workflow name is given, use it. Otherwise, design a custom sequence.
2. **Insert quality gates** — Between steps, define pass/fail criteria. A failed gate stops the workflow and reports what needs fixing.
3. **Document the flow** — Produce a clear step-by-step with inputs, outputs, and gate conditions.
4. **Execute or save** — If asked to execute, run each step sequentially. If asked to save, output the workflow definition for reuse.

## Predefined Workflows

- **implement-and-ship**: `design:spec → build:implement → build:test → build:fix (if needed) → ship:commit → ship:pr`
- **audit-sweep**: `audit:security → audit:deps → audit:compliance → audit:debt`
- **production-ready**: `operate:healthcheck → operate:monitor → operate:runbook → ship:deploy`
- **new-service**: `design:arch → generate:service → generate:proto → automate:hook → design:ci`
- **hotfix-flow**: `understand:debug → ship:hotfix → operate:healthcheck`
- **onboard-complete**: `onboard:project → onboard:codebase → onboard:setup`

## When Information is Insufficient

If the workflow goal is unclear, ask what outcome the user wants. If a step in the workflow fails its gate, report the failure and ask whether to fix and retry, skip, or abort.

## Output

### Workflow: [name]
```
Step 1: [command] — Gate: [condition]
  ↓ (pass)
Step 2: [command] — Gate: [condition]
  ↓ (pass)
Step 3: [command] — Done
```

### Gate Definitions
| Gate | Pass Condition | Failure Action |
|------|---------------|----------------|

### Execution Plan
Sequential steps with estimated time per step

## Constraints

- Gates MUST be binary (pass/fail) — no "warn and continue"
- Each step MUST produce output that the next step can consume
- If any gate fails, STOP and report — never skip gates silently
- Maximum 8 steps per workflow — longer chains should be split into sub-workflows
- Include estimated total time for the complete workflow
- Workflows must be idempotent — safe to re-run from any failed step
