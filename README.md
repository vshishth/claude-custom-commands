# Custom Claude Commands

Reusable command prompts for Claude Code, organized by workflow stage.

## Commands

### Understand — "What is this? Why is it broken?"
| Command | Description |
|---------|-------------|
| `/explain` | Explain unfamiliar code, trace logic, clarify architecture |
| `/debug` | Systematic root cause analysis from error messages or stack traces |
| `/investigate` | Investigate a bug from vague symptoms, logs, or error reports |

### Build — "Make it work, make it right, make it fast"
| Command | Description |
|---------|-------------|
| `/implement` | Implement a feature from a description, issue, or spec |
| `/fix` | Fix lint errors, type errors, or failing tests |
| `/refactor` | Safe, incremental refactoring with behavior preservation |
| `/test` | Generate meaningful tests with proper coverage strategy |
| `/perf` | Identify bottlenecks and provide concrete optimizations |

### Ship — "Get it out the door"
| Command | Description |
|---------|-------------|
| `/commit` | Conventional commit messages from staged changes |
| `/pr` | Commit, branch, push, and open a draft PR |
| `/sync` | Merge latest main/develop and resolve conflicts |
| `/pr-fix` | Resolve open PR review comments |
| `/review` | Comprehensive code review with severity ratings |
| `/deploy` | Deployment strategy with rollback capabilities |
| `/docker` | Production-ready multi-stage Dockerfiles |

### Design — "Plan before you build"
| Command | Description |
|---------|-------------|
| `/arch` | Design new systems or evaluate existing architecture |
| `/spec` | Technical design documents with goals, risks, and rollout |
| `/api` | REST or GraphQL API design with contracts and docs |
| `/adr` | Architecture Decision Records |
| `/migration` | Safe, zero-downtime database migration scripts |
| `/infra` | IaC templates (Terraform, CloudFormation, Pulumi) |
| `/ci` | CI/CD pipeline configuration for any platform |

### Audit — "Is it healthy?"
| Command | Description |
|---------|-------------|
| `/security` | Security vulnerability assessment with CWE references |
| `/deps` | Dependency health, CVEs, bloat detection, upgrade planning |
| `/debt` | Technical debt assessment with prioritized paydown plan |
| `/docs` | Generate documentation for code, APIs, or projects |
| `/release` | Structured release notes from git history |

## Usage

```bash
# In Claude Code, type the command name with a forward slash
/commands:understand:explain src/auth/login.ts
/commands:build:fix
/commands:ship:commit
/commands:audit:security src/api/
```

## Design Principles

- **Workflow-first**: Categories mirror how engineers think — understand, build, ship, design, audit
- **Short names**: Frequently-used commands are fast to type (`/commit`, `/pr`, `/fix`)
- **Focused**: Each command does one thing well in ~30-40 lines
- **Practical**: Every command produces actionable output, not generic advice
- **Composable**: Commands chain naturally (explain -> implement -> test -> commit -> pr)

## Creating New Commands

See `templates/command-template.md` for the structure. Keep commands concise and trust the model to fill in domain knowledge.
