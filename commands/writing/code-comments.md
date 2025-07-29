---
description: Generate comprehensive code comments following best practices
argument-hint: code to document with comments
allowed-tools: Read, Task
---

# Professional Code Comments Generator

## Instructions

I'll generate clear, helpful comments for the following code:

```
$ARGUMENTS
```

## Commenting Approach

1. **Comment Purpose Selection**
   - Purpose explanation (WHY)
   - Design decisions and rationale
   - Algorithm explanation
   - Non-obvious behavior notes
   - Performance considerations
   - Edge case handling
   - Usage guidance

2. **Comment Level Determination**
   - File/module level documentation
   - Class/type documentation
   - Function/method documentation
   - Complex code block explanation
   - Line-level clarification (minimal)

3. **Documentation Standard Application**
   - Language-appropriate doc format (JSDoc, PyDoc, XML Doc, etc.)
   - Parameter and return type documentation
   - Exception documentation
   - Example usage
   - References to related components

## Documentation Quality Principles

### Clarity
- Plain language explanations
- Avoidance of redundant comments
- Focus on non-obvious aspects
- Consistent terminology

### Completeness
- All public APIs documented
- Edge cases noted
- Pre/post conditions specified
- Invariants documented

### Maintainability
- Comments that add value beyond the code
- Focused on WHY not WHAT
- Abstraction-level appropriate detail
- Avoidance of comment duplication

## Comment Format

For each language, appropriate documentation format will be used:

### Classes/Types
- Purpose and responsibility
- Usage patterns
- Lifecycle information
- Thread safety notes

### Methods/Functions
- Purpose
- Parameters with constraints
- Return values
- Side effects
- Exceptions thrown
- Usage examples

### Complex Logic
- Algorithm explanation
- Performance characteristics
- Edge case handling