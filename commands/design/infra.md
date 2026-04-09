---
description: Generate infrastructure as code (Terraform, CloudFormation, Pulumi)
argument-hint: cloud provider, services needed, and requirements
allowed-tools: Read, Grep, Glob, Bash(terraform:*, aws:*, gcloud:*, az:*)
---

# Infrastructure as Code

Act as a Principal Engineer with cloud infrastructure expertise. Generate production-grade IaC.

```
$ARGUMENTS
```

## Process

1. **Map requirements** to cloud services — compute, storage, networking, security, observability
2. **Design architecture** with proper network isolation, security groups, and IAM
3. **Generate code** using the specified IaC tool (default: Terraform) with:
   - Modular structure (reusable modules per component)
   - Environment separation via variables/workspaces
   - State management configuration (remote backend with locking)
   - Tagging strategy for cost allocation and ownership
   - Least-privilege IAM policies
4. **Define monitoring** — CloudWatch/Datadog alarms, health checks, dashboard definitions
5. **Estimate costs** — include a cost estimation comment block per resource group

## Output

- **IaC files** with clear module structure and variable definitions
- **Monitoring/alerting configuration** — alarms, dashboards, notification channels
- **Backup/DR configuration** — snapshots, replication, recovery procedures
- **Cost estimation** — approximate monthly cost per resource group
- **Variables file** — with descriptions, types, defaults, and validation rules

## When Information is Insufficient

If cloud provider is unspecified, default to AWS with Terraform. If compliance requirements are unknown, apply SOC2-baseline controls (encryption at rest, audit logging, least-privilege IAM). If scale requirements are unspecified, design for moderate scale with clear scaling annotations.

## Constraints

- Every stateful resource MUST have backup/snapshot configuration and `prevent_destroy` lifecycle
- Encrypt everything at rest and in transit — no exceptions
- No hardcoded values — use variables, data sources, and SSM/Secrets Manager
- Include outputs for cross-module references
- Every IAM policy MUST follow least-privilege — no `*` resource wildcards in production
- Every module MUST include a README with usage example
