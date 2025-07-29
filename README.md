# Custom Claude Commands

This repository contains custom commands for Claude Desktop, allowing you to extend Claude's functionality with personalized workflows and automations.

## What are Custom Commands?

Custom commands in Claude Desktop allow you to create reusable prompts and workflows that can be triggered with simple shortcuts. They help streamline repetitive tasks and provide consistent, structured interactions with Claude.

## Repository Structure

```
.
├── README.md           # This file
├── commands/          # Directory for individual command files
├── templates/         # Reusable command templates
└── examples/          # Example commands for reference
```

## Command Format

Custom commands are typically defined in JSON or YAML format with the following structure:

```json
{
  "name": "command-name",
  "description": "Brief description of what this command does",
  "prompt": "The actual prompt or instruction for Claude",
  "parameters": {
    "param1": "Description of parameter 1",
    "param2": "Description of parameter 2"
  },
  "category": "development|writing|analysis|other"
}
```

## Getting Started

1. **Clone this repository** to your local machine
2. **Create your first command** in the `commands/` directory
3. **Test your command** with Claude Desktop
4. **Share and iterate** on your commands

## Command Categories

### Development
- Code review and analysis
- Documentation generation
- Testing assistance
- Debugging help

### Writing
- Content creation
- Editing and proofreading
- Style guides
- Template generation

### Analysis
- Data interpretation
- Research assistance
- Report generation
- Comparative analysis

### Productivity
- Task planning
- Meeting summaries
- Email drafting
- Project management

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
```json
{
  "name": "code-review",
  "description": "Perform a comprehensive code review",
  "prompt": "Please review the following code for:\n- Code quality and best practices\n- Potential bugs or issues\n- Performance considerations\n- Security vulnerabilities\n- Suggestions for improvement\n\nCode:\n{code}",
  "parameters": {
    "code": "The code to be reviewed"
  },
  "category": "development"
}
```

### Meeting Summary Command
```json
{
  "name": "meeting-summary",
  "description": "Generate a structured meeting summary",
  "prompt": "Create a professional meeting summary with:\n- Key decisions made\n- Action items with owners\n- Next steps\n- Important discussion points\n\nMeeting notes:\n{notes}",
  "parameters": {
    "notes": "Raw meeting notes or transcript"
  },
  "category": "productivity"
}
```

## Installation and Usage

1. **Save commands** in the appropriate directory structure
2. **Import into Claude Desktop** following the application's custom command import process
3. **Use commands** by typing the command name or using the designated shortcut

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
