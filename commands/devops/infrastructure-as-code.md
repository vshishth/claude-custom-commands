---
description: Generate infrastructure as code templates for various cloud providers
argument-hint: application requirements, cloud provider, and architectural needs
allowed-tools: Read, Task, Glob
---

# Infrastructure as Code Generator

## Instructions

I'll create infrastructure as code templates based on:

```
$ARGUMENTS
```

## Analysis Process

1. **Requirements Analysis**
   - Workload characteristics
   - Scalability needs
   - High availability requirements
   - Security constraints
   - Compliance requirements
   - Budget considerations
   - Geographic distribution

2. **Architecture Design**
   - Component identification
   - Service selection
   - Network topology
   - Security boundaries
   - Data flow mapping
   - Integration points
   - Failure domain isolation

3. **Resource Planning**
   - Compute sizing strategy
   - Storage architecture
   - Database selection
   - Caching strategy
   - Content delivery approach
   - Backup and recovery design
   - Disaster recovery planning

## Infrastructure Code Generation

### Core Infrastructure
- VPC/Network design
- Subnet architecture
- Security group definitions
- IAM/RBAC configuration
- Load balancer setup
- Auto-scaling configuration
- DNS management

### Compute Resources
- Instance/container definitions
- Kubernetes manifest generation
- Serverless function templates
- Spot instance strategy
- Instance profile configuration
- Host security hardening

### Data Storage
- Database infrastructure
- Storage service configuration
- Backup automation
- Replication setup
- Encryption implementation
- Data lifecycle management
- Performance optimization

### Security Implementation
- Network ACLs
- WAF configuration
- Secret management
- Private link/endpoint setup
- Logging and monitoring
- Compliance controls
- Identity federation

### Operational Tooling
- Monitoring infrastructure
- Log aggregation setup
- Alerting configuration
- Metrics collection
- Dashboard templates
- Incident management integration

## Deployment Management

### State Management
- Backend configuration
- State locking implementation
- Resource dependency mapping
- Resource naming strategy
- Tagging policy

### CI/CD Integration
- Pipeline configuration
- Validation workflow
- Approval gates
- Drift detection
- Automated testing

### Environment Separation
- Development environment
- Staging configuration
- Production hardening
- Multi-account strategy
- Resource isolation approach

## Cost Optimization

### Resource Efficiency
- Right-sizing recommendations
- Reserved capacity strategy
- Spot usage opportunities
- Auto-scaling policies
- Idle resource detection

### Cost Control
- Budget implementation
- Cost allocation tagging
- Usage monitoring
- Anomaly detection
- Savings plans strategy

## Implementation Strategy

### Deployment Plan
- Resource sequencing
- Dependency management
- Rollout strategy
- Testing approach
- Validation criteria

### Documentation
- Architecture diagrams
- Resource inventory
- Configuration reference
- Operational runbooks
- Security controls