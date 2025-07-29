---
description: Generate database migration scripts for schema changes
argument-hint: database type, current schema, and desired changes
allowed-tools: Read, Task, Glob
---

# Database Migration Generator

## Instructions

I'll generate optimal database migration scripts based on:

```
$ARGUMENTS
```

## Analysis Process

1. **Schema Analysis**
   - Current schema examination
   - Target schema identification
   - Difference analysis
   - Constraint evaluation
   - Dependency mapping

2. **Migration Strategy Design**
   - Data preservation approach
   - Backward compatibility assessment
   - Performance impact analysis
   - Transaction boundary planning
   - Rollback strategy development

3. **Risk Assessment**
   - Downtime requirements
   - Data integrity risks
   - Performance implications
   - Application compatibility issues
   - Potential failure points

## Migration Script Generation

### Schema Changes
- Table creation/modification/removal scripts
- Column additions/modifications/removals
- Index creation/optimization/removal
- Constraint management
- View updates

### Data Migration
- Data transformation scripts
- Default value application
- Referential integrity maintenance
- Temporary structure usage
- Batch processing approach

### Performance Optimization
- Index usage during migration
- Lock minimization strategy
- Batching recommendations
- Parallelization opportunities
- Resource allocation guidance

### Safety Measures
- Transaction management
- Validation queries
- Integrity checks
- Rollback scripts
- State verification

### Database-Specific Optimizations
- Platform-specific features utilization
- Vendor-specific best practices
- Tool integration opportunities
- Engine-specific syntax

## Deployment Strategy

### Pre-Migration Tasks
- Backup requirements
- Application preparation
- Dependency verification
- Environment preparation
- Notification requirements

### Execution Plan
- Timing recommendations
- Monitoring approach
- Progress tracking
- Verification steps
- Go/no-go criteria

### Post-Migration Verification
- Data integrity validation
- Performance validation
- Application compatibility verification
- Monitoring recommendations
- Issue detection queries

### Rollback Plan
- Complete rollback scripts
- Point-of-no-return identification
- Partial rollback strategies
- Recovery time objectives
- Data reconciliation approach

## Integration Recommendations

### ORM Integration
- Framework-specific migration adapters
- Model updates
- Code generation recommendations
- Version control strategies

### CI/CD Integration
- Automated testing approach
- Integration test recommendations
- Staging environment requirements
- Production deployment guidelines