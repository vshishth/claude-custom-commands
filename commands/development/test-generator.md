---
description: Generate comprehensive tests for your code
argument-hint: code to test and preferred testing framework
allowed-tools: Read, Grep, Glob
---

# Test Generator

## Instructions

I'll generate comprehensive tests for the following code:

```
$ARGUMENTS
```

## Testing Approach

1. **Test Coverage Analysis**
   - Identify all functions/methods to test
   - Determine branches requiring coverage
   - Map out edge cases and boundary conditions
   - Note expected behavior for error conditions

2. **Test Types Generation**
   - Unit tests for individual functions
   - Integration tests for component interactions
   - Edge case tests
   - Performance tests (if applicable)
   - Security tests (if applicable)

3. **Test Structure**
   - Test setup and teardown
   - Mocks and stubs for dependencies
   - Test data generation
   - Assertion patterns

## Testing Framework Customization

Tests will be generated using the framework mentioned in your input, or I'll recommend an appropriate one based on your code's language and structure.

## Generated Tests

Each test will include:
1. Clear description of what's being tested
2. Proper setup with required context
3. Test execution with appropriate assertions
4. Cleanup/teardown as needed
5. Comments explaining the test's purpose

## Test Organization

Tests will be structured by:
1. Functional area
2. Component
3. Test type (happy path, edge cases, error handling)

## Coverage Assessment

The tests will aim to achieve:
1. High line coverage
2. Full branch coverage
3. Comprehensive edge case handling
4. Error condition testing