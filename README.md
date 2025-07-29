# Custom Claude Commands

This repository contains custom commands for Claude Desktop, allowing you to extend Claude's functionality with personalized workflows and automations.

## What are Custom Commands?

Custom commands in Claude Desktop allow you to create reusable prompts and workflows that can be triggered with simple shortcuts. They help streamline repetitive tasks and provide consistent, structured interactions with Claude.

## Repository Structure

```
.
├── README.md                              # This file
├── commands/                             # Directory for individual command files
│   ├── development/                      # Development-related commands
│   │   ├── architecture.md               # System architecture design & evaluation
│   │   ├── code-review.md                # Comprehensive code review
│   │   ├── debug.md                      # Advanced debugging assistance
│   │   ├── refactor.md                   # Code refactoring planning
│   │   └── test-generator.md             # Comprehensive test generation
│   ├── productivity/                     # Productivity enhancement commands
│   │   ├── daily-standups.md             # Generate standups updates
│   │   ├── git-commit.md                 # Create well-structured git commits
│   │   ├── meeting-notes.md              # Structure and summarize meeting notes
│   │   ├── project-plan.md               # Create detailed project plans
│   │   └── task-breakdown.md             # Break down complex tasks
│   ├── analysis/                         # Analysis and evaluation commands
│   │   ├── code-quality.md               # Analyze codebase quality metrics
│   │   ├── dependency-analysis.md        # Analyze project dependencies
│   │   ├── performance-analysis.md       # Find performance bottlenecks
│   │   └── security-audit.md             # Security vulnerability assessment
│   └── writing/                          # Documentation and content commands
│       ├── code-comments.md              # Generate professional code comments
│       ├── documentation.md              # Create comprehensive documentation
│       ├── release-notes.md              # Generate structured release notes
│       ├── technical-spec.md             # Create detailed technical specs
│       └── user-stories.md               # Generate user stories
├── templates/                           # Reusable command templates
│   └── command-template.md              # Template for creating new commands
└── examples/                            # Example commands for reference
    └── git-workflow.md                  # Git workflow assistant example
```

## Command Format

Custom Claude commands are defined in Markdown format with YAML frontmatter:

```markdown
---
description: Brief description of what this command does
argument-hint: Description of expected input (optional)
allowed-tools: Tools the command can use (comma-separated, optional)
---

# Command Name

## Instructions

I'll help you with [specific task] based on:

```
$ARGUMENTS
```

## Process
[Command content that processes the input and generates the desired output]
```

The `$ARGUMENTS` placeholder is automatically replaced with the user's input when the command is executed.

## Getting Started

1. **Clone this repository** to your local machine
2. **Create your first command** in the `commands/` directory
3. **Test your command** with Claude Desktop
4. **Share and iterate** on your commands

## Command Categories

### Development
- **Code Review** - Comprehensive code quality and security analysis
- **Architecture** - Design system architecture or evaluate existing architecture
- **Debug** - Advanced debugging assistance for identifying and fixing issues
- **Refactor** - Generate refactoring plans to improve code quality
- **Test Generator** - Create comprehensive tests for your code

### Productivity
- **Git Commit** - Create well-structured git commits using conventional format
- **Meeting Notes** - Structure and summarize meeting notes with action items
- **Project Plan** - Create detailed project plans with tasks and timelines
- **Daily Standups** - Generate structured daily standup updates
- **Task Breakdown** - Break down complex tasks into manageable subtasks

### Analysis
- **Code Quality** - Analyze codebase quality metrics and suggest improvements
- **Dependency Analysis** - Analyze project dependencies and identify risks
- **Performance Analysis** - Find performance bottlenecks and optimization opportunities
- **Security Audit** - Perform comprehensive security vulnerability assessment

### Writing
- **Documentation** - Generate comprehensive project or code documentation
- **Release Notes** - Create structured release notes from git history
- **Technical Spec** - Write detailed technical specifications for features
- **Code Comments** - Generate professional code comments following best practices
- **User Stories** - Create structured user stories from requirements

## Best Practices

1. **Clear Naming**: Use descriptive, kebab-case names for your commands
2. **Detailed Descriptions**: Provide clear descriptions of what each command does
3. **Parameter Documentation**: Document all parameters and their expected formats
4. **Version Control**: Track changes to your commands over time
5. **Testing**: Test commands thoroughly before sharing
6. **Documentation**: Keep this README updated as you add new commands

## Contributing

1. Fork this repository
2. Create a new branch for your command
3. Add your command with proper documentation
4. Test the command thoroughly
5. Submit a pull request with a clear description

## Command Examples

### Code Review Command
```markdown
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

[Additional review sections...]
```

### Meeting Notes Command
```markdown
---
description: Structure and summarize meeting notes with action items
argument-hint: raw meeting notes or transcript
allowed-tools: Task
---

# Meeting Notes Organizer

## Instructions

I'll organize and structure the following meeting notes into a clear, actionable summary:

```
$ARGUMENTS
```

## Analysis Process

1. **Meeting Content Analysis**
   - Identify key discussion topics
   - Extract decisions made
   - Capture action items and owners
   - Note important insights and concerns
   - Recognize unresolved questions

[Additional sections...]
```

## Installation and Usage

1. **Clone this repository** to your local machine
2. **Copy commands** to your Claude commands directory:
   - Personal commands: `~/.claude/commands/`
   - Project-level commands: `.claude/commands/` in your project directory
3. **Use commands** by typing the command name with a forward slash, e.g., `/code-review`
4. **Provide arguments** directly after the command or in a new message

For more information on Claude commands, see the [official documentation](https://docs.anthropic.com/en/docs/claude-code/slash-commands).

## Troubleshooting

- **Command not working**: Check JSON/YAML syntax
- **Parameters not recognized**: Verify parameter names match usage
- **Unexpected output**: Review prompt clarity and specificity

## Resources

- [Claude Desktop Documentation](https://claude.ai/desktop)
- [Custom Commands Guide](https://docs.anthropic.com/claude/custom-commands)
- [Community Examples](https://github.com/anthropics/claude-custom-commands)

## License

This repository is licensed under the MIT License. See LICENSE file for details.

## Support

For questions or issues:
1. Check existing issues in this repository
2. Create a new issue with detailed description
3. Join the community discussions

---

**Happy commanding!** 🚀
