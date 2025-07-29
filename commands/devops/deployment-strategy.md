---
description: Design deployment strategies for applications with rollback capabilities
argument-hint: application type, target environment, availability requirements
allowed-tools: Read, Task, Glob
---

# Deployment Strategy Designer

## Instructions

I'll design a comprehensive deployment strategy based on:

```
$ARGUMENTS
```

## Analysis Process

1. **Application Analysis**
   - Architecture evaluation
   - State management assessment
   - Database dependency mapping
   - Service dependency identification
   - Traffic pattern analysis
   - Downtime sensitivity

2. **Environment Assessment**
   - Infrastructure capability analysis
   - Scaling requirements
   - High availability needs
   - Geographic distribution
   - Compliance constraints
   - Disaster recovery requirements

3. **Risk Profile Development**
   - Critical failure points
   - Recovery time objectives
   - Service level agreements
   - Business impact assessment
   - Acceptable downtime windows
   - Data integrity requirements

## Deployment Strategy Design

### Strategy Selection
- Blue/Green deployment
- Canary releases
- Rolling updates
- Feature toggles
- Shadow deployments
- A/B testing approach
- Traffic shifting patterns

### Deployment Workflow
- Build artifact management
- Environment promotion flow
- Approval gates
- Automated validation
- Monitoring integration
- Notification system

### Configuration Management
- Environment-specific configuration
- Secrets management
- Feature flag framework
- Dynamic configuration approach
- Configuration validation

### Rollback Mechanisms
- Automated rollback triggers
- Data migration reversibility
- State reconciliation approach
- Recovery point objectives
- Recovery time targets
- Rollback testing strategy

### Health Verification
- Health check implementation
- Smoke test design
- Synthetic transaction monitoring
- Performance baseline verification
- Security validation

## Implementation Plan

### Infrastructure Requirements
- Load balancer configuration
- Database replication needs
- Cache warming strategy
- Service discovery updates
- DNS management approach
- Network configuration

### Automation Requirements
- CI/CD pipeline integration
- Automated testing needs
- Approval workflow
- Notification requirements
- Monitoring integration

### Operation Procedures
- Deployment runbooks
- Communication templates
- Escalation procedures
- Incident response plan
- Post-deployment verification checklist
- Blameless postmortem framework

### Metrics and Monitoring
- Deployment success metrics
- Performance monitoring
- Error rate tracking
- Business impact metrics
- Deployment time tracking
- Recovery time measurements

## Risk Mitigation

### Failure Scenarios
- Network partition handling
- Database unavailability strategy
- Dependency failure management
- Traffic spike handling
- Corrupted deployment recovery
- Incomplete deployment reconciliation

### Testing Strategy
- Chaos engineering approach
- Failure injection methodology
- Recovery verification
- Performance under stress
- Resilience validation