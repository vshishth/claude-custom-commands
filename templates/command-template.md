---
description: Template for creating new Claude commands
---

# Command Template Guide

## Basic Command Structure

```markdown
---
description: Clear, concise description of what this command does
argument-hint: Description of expected input (optional)
allowed-tools: Tools the command can use (optional, comma-separated)
---

# Command Name

## Instructions

I'll help you with [specific task] based on:

```
$ARGUMENTS
```

## Process Steps

1. **Step 1 Name**
   - Substep detail
   - Substep detail

2. **Step 2 Name**
   - Substep detail
   - Substep detail

## Output Structure

### Section 1
[Description of what goes here]

### Section 2
[Description of what goes here]

## Additional Information
[Optional sections, customizations, etc.]
```

## YAML Frontmatter Options

### Required Fields
- `description`: Concise summary of the command's purpose

### Optional Fields
- `argument-hint`: Guidance on what input to provide
- `allowed-tools`: Specific tools the command can use
- `private`: Set to `true` to hide from listings (default: false)

## Best Practices

1. **Clear Purpose**
   - Each command should do one thing well
   - Focus on specific use cases

2. **Structured Output**
   - Use consistent formatting
   - Organize information logically
   - Use markdown for readability

3. **Dynamic Content**
   - Use `$ARGUMENTS` to capture user input
   - Use `!` prefix for bash commands
   - Use `@` prefix for file references

4. **Maintainability**
   - Include clear documentation
   - Version your commands
   - Group related commands