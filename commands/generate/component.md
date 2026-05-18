---
description: Generate React/frontend components with tests, stories, and proper typing
argument-hint: component description (e.g., "ReservationCard - displays reservation details with status badge")
allowed-tools: Read, Grep, Glob, Bash(npm:*, npx:*, find:*, mkdir:*, ls:*)
---

# Generate Component

Act as a Principal Engineer scaffolding a frontend component. Match the exact patterns and conventions in the existing codebase — never impose external style.

Component patterns:
!`find . -path "*/components/*" -name "*.tsx" | head -10 2>/dev/null`

Testing setup:
!`find . -name "*.test.tsx" -o -name "*.spec.tsx" -o -name "*.stories.tsx" | head -5 2>/dev/null`

Styling approach:
!`grep -rl "styled-components\|tailwind\|css-modules\|emotion\|scss" --include="*.tsx" --include="*.json" -l 2>/dev/null | head -5`

```
$ARGUMENTS
```

## Process

1. **Detect conventions** — Find existing components and identify: file structure (flat vs co-located), naming (PascalCase file, index barrel), styling approach, prop typing patterns, test patterns.
2. **Generate component** — Create the component file with proper TypeScript props interface, matching the styling approach and composition patterns.
3. **Generate tests** — Create test file with: render test, prop variations, interaction tests, accessibility checks.
4. **Generate stories** — If Storybook is detected, create a stories file with variants.
5. **Export** — Wire the component into the appropriate barrel export or index file.

## When Information is Insufficient

If the component description is vague, ask for: props, visual behavior, interactions, and where it fits in the page hierarchy. If no existing components exist, ask for framework (React/Vue/Svelte) and styling preference.

## Output

### Files Created
- Component: [path]
- Tests: [path]
- Stories: [path] (if Storybook detected)
- Types: [path] (if separate types file pattern)

### Props Interface
```typescript
interface Props { ... }
```

### Usage Example
```tsx
<ComponentName prop={value} />
```

## Constraints

- MUST include TypeScript prop types — no `any` types
- MUST include at least one render test and one interaction test
- MUST match existing styling approach — don't mix Tailwind and CSS modules
- NEVER use inline styles unless that's the project convention
- Include accessibility attributes (aria-labels, roles) for interactive elements
- Follow the project's state management pattern (controlled vs uncontrolled)
