# Custom Claude Commands

Reusable command prompts for Claude Code, organized by developer lifecycle stage. Every command enforces Principal Engineer standards. **55 commands** across **10 categories**.

## Developer Lifecycle

```
Onboard → Understand → Design → Generate → Build → Ship → Operate → Audit → Manage → Automate
```

## Commands

### Onboard — "Get productive fast"
| Command | Description |
|---------|-------------|
| `/project` | Discover stack, key files, conventions, and team context |
| `/codebase` | Generate codebase map with architecture overview and module boundaries |
| `/setup` | Validate and guide local development environment setup |

### Understand — "What is this? Why is it broken?"
| Command | Description |
|---------|-------------|
| `/explain` | Explain unfamiliar code, trace logic, clarify architecture |
| `/debug` | Systematic root cause analysis from error messages or stack traces |
| `/investigate` | Investigate a bug from vague symptoms, logs, or error reports |
| `/trace` | Distributed trace analysis across multi-service hops |
| `/cost` | Cloud cost analysis and optimization recommendations |

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
| `/event` | Event-driven architecture: schemas, pub/sub, event flows |

### Generate — "Scaffold, don't start from scratch"
| Command | Description |
|---------|-------------|
| `/service` | Scaffold a new microservice (Go gRPC or TS) with standard structure |
| `/endpoint` | Generate API endpoint with handler, validation, tests, route registration |
| `/model` | Generate data models with migrations and repository layer |
| `/proto` | Generate protobuf definitions and client/server stubs |
| `/component` | Generate React/frontend components with tests and stories |

### Build — "Make it work, make it right, make it fast"
| Command | Description |
|---------|-------------|
| `/implement` | Implement a feature from a description, issue, or spec |
| `/fix` | Fix lint errors, type errors, or failing tests |
| `/refactor` | Safe, incremental refactoring with behavior preservation |
| `/test` | Generate meaningful tests with proper coverage strategy |
| `/perf` | Identify bottlenecks and provide concrete optimizations |
| `/bench` | Benchmarking with regression detection and historical comparison |

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
| `/hotfix` | Emergency hotfix: branch from release, cherry-pick, fast-track PR |

### Operate — "Keep it running"
| Command | Description |
|---------|-------------|
| `/healthcheck` | Verify service health across environments; check endpoints, deps, secrets |
| `/incident` | Generate incident response playbook with triage and post-mortem |
| `/runbook` | Generate operational runbooks from code and deploy configs |
| `/monitor` | Design observability: metrics, logs, traces, alerts, dashboards |
| `/rollback` | Guided rollback procedure based on deployment type |

### Audit — "Is it healthy?"
| Command | Description |
|---------|-------------|
| `/security` | Security vulnerability assessment with CWE references |
| `/deps` | Dependency health, CVEs, bloat detection, upgrade planning |
| `/debt` | Technical debt assessment with prioritized paydown plan |
| `/docs` | Generate documentation for code, APIs, or projects |
| `/release` | Structured release notes from git history |
| `/compliance` | License compliance, SBOM validation, policy enforcement |

### Manage — "Control your environments"
| Command | Description |
|---------|-------------|
| `/env` | Audit, diff, and sync environment variables across environments |
| `/secrets` | Chamber/SSM secret management: rotate, audit, bootstrap, validate |
| `/deps-update` | Automated dependency updates with compatibility analysis |
| `/version` | Semantic versioning: bump, changelog, tag management |
| `/config` | Configuration drift detection between environments |

### Automate — "Never do it twice"
| Command | Description |
|---------|-------------|
| `/hook` | Set up git hooks (pre-commit, pre-push, commit-msg) per project type |
| `/workflow` | Create compound multi-step workflows with quality gates |
| `/schedule` | Set up recurring automated tasks |
| `/guard` | Define and run quality gates that must pass before shipping |

## Usage

```bash
# In Claude Code, type the command category and name
/commands:onboard:project
/commands:understand:explain src/auth/login.ts
/commands:generate:endpoint POST /api/reservations
/commands:build:fix
/commands:ship:commit
/commands:operate:healthcheck
/commands:audit:security src/api/
/commands:manage:secrets audit staging
/commands:automate:guard pre-merge
```

## Composition Chains

Commands chain naturally across lifecycle stages:

```
# New developer onboarding
onboard:project → onboard:codebase → onboard:setup

# Feature implementation
design:spec → generate:endpoint → build:test → ship:pr

# Production incident
understand:trace → operate:incident → ship:hotfix → operate:healthcheck

# Audit sweep
audit:security → audit:deps → audit:compliance → audit:debt

# New service
design:arch → generate:service → generate:proto → automate:hook → design:ci

# Release
manage:version → audit:release → ship:deploy → operate:healthcheck

# Compound (use /automate:workflow)
implement-and-ship: build:implement → build:test → ship:commit → ship:pr
```

## Command Quality Standards

Every command in this collection enforces:
- **Principal Engineer role** — operates with senior technical judgment
- **Ambiguity handling** — explicit behavior when inputs are incomplete
- **Scoped tool access** — `allowed-tools` narrowly scoped (no bare `Bash`)
- **Structured output** — deterministic, actionable output with concrete fixes
- **Safety guards** — destructive commands require explicit confirmation

## Design Principles

- **Lifecycle-first**: Categories mirror the full engineering lifecycle — onboard through automate
- **Short names**: Frequently-used commands are fast to type (`/commit`, `/pr`, `/fix`)
- **Focused**: Each command does one thing well in ~45-65 lines
- **Practical**: Every command produces actionable output, not generic advice
- **Composable**: Commands chain naturally across lifecycle stages
- **Convention-driven**: Generate/scaffold commands copy existing codebase patterns

## Creating New Commands

See `templates/command-template.md` for the structure. New commands must:
- Use the canonical structure (frontmatter → role → context → process → ambiguity → output → constraints)
- Scope `allowed-tools` narrowly
- Include a "When Information is Insufficient" section
- Require concrete fixes in output, not generic advice
- Use "Constraints" for hard rules
