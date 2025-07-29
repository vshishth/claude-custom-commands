---
description: Generate a refactoring plan and implementation for improving code quality
argument-hint: file_path or paste code directly
allowed-tools: Read, Grep, Glob, Task
---

# Code Refactoring Plan & Implementation

## Instructions

Analyze the following code and provide a comprehensive refactoring plan focused on improving quality while preserving functionality:

```
$ARGUMENTS
```

## Refactoring Analysis

1. **Code Structure Assessment**
   - Identify overly complex methods/functions
   - Detect code duplication
   - Find tightly coupled components
   - Locate unclear abstractions
   - Note poor separation of concerns

2. **Refactoring Opportunities**
   - Extract method/function opportunities
   - Class/module restructuring needs
   - Interface improvements
   - Design pattern applications
   - Performance optimization points

3. **Code Quality Issues**
   - Naming improvements
   - Comment/documentation needs
   - Testing gaps
   - Error handling weaknesses

## Refactoring Plan

For each identified issue:
1. Describe the current problem concisely
2. Explain why it needs refactoring (maintainability, performance, etc.)
3. Provide a clear refactoring strategy
4. Show a "before and after" code comparison

## Implementation Steps

Present a sequential list of refactoring steps:
1. Start with the simplest, safest changes
2. Progress to more complex transformations
3. Include test/verification steps between major changes
4. Note potential risks and mitigation strategies

## Refactored Code

Provide the complete refactored implementation with:
1. Clean, well-structured code
2. Improved naming and organization
3. Appropriate comments/documentation
4. Preserved functionality