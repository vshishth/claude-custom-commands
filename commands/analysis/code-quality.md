---
description: Analyze codebase quality metrics and provide improvement recommendations
argument-hint: repo path or specific files to analyze
allowed-tools: Read, Grep, Glob, Task
---

# Code Quality Analysis

## Instructions

I'll analyze the quality of the following codebase or files:

```
$ARGUMENTS
```

## Analysis Process

1. **Code Metrics Assessment**
   - Complexity metrics (cyclomatic complexity, cognitive complexity)
   - Size metrics (LOC, method length, class size)
   - Coupling and cohesion analysis
   - Duplication detection
   - Comment ratio and quality
   - Code style consistency

2. **Pattern Detection**
   - Anti-pattern identification
   - Code smells
   - Potential bugs
   - Maintainability issues
   - Performance concerns
   - Security vulnerabilities

3. **Architecture Evaluation**
   - Component organization
   - Dependency structure
   - Separation of concerns
   - Interface design
   - Abstraction quality

## Quality Report

### Executive Summary
- Overall quality assessment
- Key strengths
- Critical areas for improvement
- Technical debt estimate

### Detailed Findings
For each area:
1. Current state
2. Issues identified
3. Impact assessment
4. Priority rating

### Heat Map
- Files/components with highest risk
- Technical debt hotspots
- Complexity centers

## Improvement Plan

### Immediate Actions
- Critical issues requiring immediate attention
- Quick wins with high impact

### Mid-term Improvements
- Structural refactorings
- Pattern remediation
- Test coverage increases

### Long-term Strategy
- Architectural improvements
- Process changes
- Quality governance recommendations

## Implementation Roadmap
- Phased approach to improvements
- Estimated effort per phase
- Success metrics