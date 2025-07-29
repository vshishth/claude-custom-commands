---
description: Analyze project dependencies, identify risks and suggest improvements
argument-hint: package.json, Gemfile, requirements.txt, etc.
allowed-tools: Read, Grep, Glob, Bash(npm list:*, pip list:*, bundle list:*, yarn list:*)
---

# Dependency Analysis

## Context

Let me analyze the dependencies in your project:

```
$ARGUMENTS
```

Installed dependencies:
!`npm list --depth=0 2>/dev/null || pip list 2>/dev/null || bundle list 2>/dev/null || yarn list --depth=0 2>/dev/null || echo "No standard dependency manager detected"`

## Analysis Process

1. **Dependency Overview**
   - Total dependencies count
   - Direct vs. transitive dependencies
   - Production vs. development dependencies
   - Major framework and library detection

2. **Risk Assessment**
   - Outdated dependencies
   - Deprecated packages
   - Security vulnerabilities
   - License compliance issues
   - Conflicting versions
   - Unused dependencies

3. **Dependency Graph**
   - Key dependency relationships
   - Dependency chains
   - Circular dependencies
   - Bottleneck packages

## Detailed Report

### Critical Dependencies
- Core frameworks
- Essential libraries
- Infrastructure components
- Testing frameworks

### Dependency Health Metrics
- Update frequency
- Community activity
- Maintenance status
- Documentation quality
- Test coverage

### Vulnerability Assessment
- Known security issues
- Potential exploit vectors
- Severity ratings
- Patch status

## Optimization Recommendations

### Immediate Actions
- Critical updates needed
- Security patches
- Breaking changes to address

### Maintenance Strategy
- Update policy recommendations
- Dependency refresh cadence
- Automated monitoring tools

### Architectural Improvements
- Dependency reduction opportunities
- Alternative package recommendations
- Modularization suggestions
- Isolation strategies for risky dependencies

## Implementation Plan
- Prioritized update sequence
- Testing requirements
- Potential impact assessment