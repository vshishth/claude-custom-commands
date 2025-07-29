---
description: Git workflow assistant for common operations
allowed-tools: Bash(git status:*, git branch:*, git diff:*)
---

# Git Workflow Assistant

## Current State
Current branch:
!`git branch --show-current`

Git status:
!`git status`

## Options

Choose one of these workflows by providing the corresponding number:

1. **View changes** - See what's changed in your working directory
2. **Stage changes** - Add modified files to staging
3. **Create commit** - Commit staged changes with a message
4. **Branch management** - Create, delete, or switch branches
5. **Merge workflow** - Merge branches with conflict resolution
6. **Stash operations** - Save or apply stashed changes
7. **Remote operations** - Push, pull, or fetch

## Selected Workflow: $ARGUMENTS

Based on your selection, I'll help you complete that git workflow with step-by-step instructions and commands.

For example, if you selected "3" for creating a commit:

1. First, let's check what's staged:
   !`git diff --staged --name-status`

2. I'll help you write a conventional commit message following the format:
   ```
   type(scope): subject
   
   body
   
   footer
   ```

3. Suggest the appropriate git commands to execute the commit

If you need help with a different workflow, please specify the number from the options above.