---
description: Cloud cost analysis and optimization recommendations
argument-hint: service, resource type, or cost concern (e.g., "RDS costs", "Lambda optimization", "overall spend")
allowed-tools: Read, Grep, Glob, Bash(aws ce get-cost-and-usage:*, aws pricing:*, find:*, grep:*, cat:*)
---

# Cloud Cost Analysis

Act as a Principal Engineer optimizing cloud spend. Analyze infrastructure code and resource configurations to identify cost reduction opportunities.

Infrastructure code:
!`find . -name "*.tf" -o -name "*.tfvars" -o -name "atmos*" -o -name "*.yaml" -path "*helm*" | head -10 2>/dev/null`

Resource definitions:
!`grep -rl "instance_type\|instance_class\|memory_size\|storage\|scaling" --include="*.tf" --include="*.yaml" 2>/dev/null | head -10`

```
$ARGUMENTS
```

## Process

1. **Inventory resources** — From Terraform/IaC files, identify provisioned resources: compute (EC2, ECS, Lambda), storage (RDS, S3, EBS), network (NAT, ALB), and managed services.
2. **Identify over-provisioning** — Check for: oversized instances, unused storage, over-provisioned databases, Lambda with excess memory, EBS volumes with low IOPS utilization.
3. **Spot optimization opportunities** — Look for: Reserved Instance candidates (steady-state workloads), Savings Plans eligibility, spot instance candidates (stateless workers), storage tier opportunities (S3 lifecycle, GP3 vs GP2).
4. **Analyze scaling configuration** — Check auto-scaling policies: are min/max values appropriate? Are scale-down policies aggressive enough? Are there idle resources during off-peak?
5. **Estimate savings** — For each recommendation, estimate monthly savings with confidence level.

## When Information is Insufficient

If no IaC files exist, analyze from Dockerfiles and deploy configs what resources are likely needed, and ask for AWS account access. If cost data isn't available, provide recommendations based on resource configuration analysis alone.

## Output

### Resource Inventory
| Resource | Type/Size | Monthly Est. | Utilization |
|----------|-----------|-------------|-------------|

### Optimization Recommendations
| # | Action | Estimated Savings | Risk | Effort |
|---|--------|------------------|------|--------|

### Quick Wins (implement today)
### Medium-Term (requires planning)
### Strategic (architecture changes)

## Constraints

- NEVER recommend changes that compromise reliability without explicit trade-off discussion
- Savings estimates MUST include confidence level (high/medium/low based on data available)
- Distinguish between dev/staging (optimize aggressively) and production (optimize carefully)
- Include rollback plan for each recommendation (can we go back if performance degrades?)
- Consider reserved instances / savings plans ONLY for stable workloads (>6 months consistent)
