---
description: Generate infrastructure as code (Terraform, CloudFormation, Pulumi)
argument-hint: cloud provider, services needed, and requirements
allowed-tools: Read, Glob
---

# Infrastructure as Code

Generate IaC templates for:

```
$ARGUMENTS
```

## Process

1. **Map requirements** to cloud services - compute, storage, networking, security
2. **Design architecture** with proper network isolation, security groups, and IAM
3. **Generate code** using the specified IaC tool (default: Terraform) with:
   - Modular structure (reusable modules per component)
   - Environment separation via variables/workspaces
   - State management configuration
   - Tagging strategy for cost allocation
   - Least-privilege IAM policies

## Principles

- Immutable infrastructure where possible
- Encrypt everything at rest and in transit
- No hardcoded values - use variables and data sources
- Include outputs for cross-module references
- Add lifecycle rules to prevent accidental deletion of stateful resources
