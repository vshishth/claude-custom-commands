---
description: Perform a comprehensive code review
argument-hint: file_path or paste code directly
allowed-tools: Read, Grep, Glob
---

# Comprehensive Code Review

## Instructions

Analyze the following code with the mindset of a senior engineer conducting a thorough code review:

```
$ARGUMENTS
```

## Review Focus Areas

1. **Code Quality**
   - Clean code principles
   - Readability and maintainability
   - Code organization and structure
   - Function/method length and complexity
   - Variable/function naming conventions
   - Comments and documentation

2. **Bugs & Issues**
   - Logic errors
   - Edge cases not handled
   - Potential null/undefined references
   - Off-by-one errors
   - Race conditions (for concurrent code)
   - Memory leaks

3. **Performance Considerations**
   - Time complexity analysis
   - Space complexity analysis
   - Efficient algorithm choices
   - Potential bottlenecks
   - Resource usage

4. **Security**
   - Input validation
   - Authorization checks
   - SQL/NoSQL injection risks
   - XSS vulnerabilities
   - Data exposure risks
   - Secure credential handling

5. **Testing**
   - Test coverage assessment
   - Missing test cases
   - Testability issues

## Review Format

For each issue identified:
1. Provide the specific line number or code snippet
2. Explain the issue clearly
3. Rate the severity (Critical, High, Medium, Low)
4. Provide a specific recommendation for improvement
5. Include sample code when appropriate

## Summary

Conclude with:
1. Overall assessment (3-5 bullet points)
2. Key strengths of the code
3. Priority improvements (top 3)
4. Any architectural considerations