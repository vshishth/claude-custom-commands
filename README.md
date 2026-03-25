# Custom Claude Commands

Reusable command prompts for Claude Code, designed around Principal Engineer workflows.

## Commands

### Development
| Command | Description |
|---------|-------------|
| `/code-review` | Comprehensive code review with severity ratings and actionable fixes |
| `/debug` | Systematic root cause analysis from error messages or stack traces |
| `/refactor` | Safe, incremental refactoring with behavior preservation |
| `/architecture` | Design new systems or evaluate existing architecture |
| `/test-generator` | Generate meaningful tests with proper coverage strategy |
| `/performance` | Identify bottlenecks and provide concrete optimizations |

### Analysis
| Command | Description |
|---------|-------------|
| `/security-audit` | Security vulnerability assessment with CWE references and fixes |
| `/dependency-analysis` | Dependency health, CVEs, bloat detection, upgrade planning |
| `/tech-debt` | Technical debt assessment with prioritized paydown plan |

### Writing
| Command | Description |
|---------|-------------|
| `/technical-spec` | Technical design documents with goals, design, risks, and rollout |
| `/adr` | Architecture Decision Records for documenting key decisions |
| `/documentation` | Generate docs for code, APIs, or projects |
| `/release-notes` | Structured release notes from git history |

### DevOps
| Command | Description |
|---------|-------------|
| `/cicd-pipeline` | CI/CD pipeline configuration for any platform |
| `/dockerfile-generator` | Production-ready multi-stage Dockerfiles |
| `/deployment-strategy` | Deployment strategies with rollback capabilities |
| `/infrastructure-as-code` | IaC templates (Terraform, CloudFormation, Pulumi) |

### Data & API
| Command | Description |
|---------|-------------|
| `/migration-generator` | Safe, zero-downtime database migration scripts |
| `/api-design` | REST or GraphQL API design with contracts and docs |

### Productivity
| Command | Description |
|---------|-------------|
| `/git-commit` | Conventional commit messages from staged changes |
| `/draft-pr` | Commit staged changes, branch, push, and open a draft PR |

## Usage

```bash
# In Claude Code, type the command name with a forward slash
/code-review src/auth/login.ts
/debug "TypeError: Cannot read property 'id' of undefined"
/security-audit src/api/
```

## Design Principles

- **Focused**: Each command does one thing well in ~30-40 lines
- **Opinionated**: Commands guide toward specific output, not exhaustive checklists
- **Practical**: Every command produces actionable output, not generic advice
- **Composable**: Commands can be chained (review -> refactor -> test-generator)

## Creating New Commands

See `templates/command-template.md` for the structure. Keep commands concise and trust the model to fill in domain knowledge.
