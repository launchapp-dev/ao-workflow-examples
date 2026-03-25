# AO Workflow Examples

Real-world workflow examples for the [AO Agent Orchestrator](https://github.com/launchapp-dev/ao-cli) — a Rust-based system that orchestrates AI agents to autonomously build, test, review, and ship code.

These examples are drawn from production systems managing 55+ repositories, 180+ PRs/week, and multiple product lines. Each demonstrates a distinct orchestration pattern you can adapt for your own projects.

## Examples

| # | Pattern | Description | Complexity |
|---|---------|-------------|------------|
| 01 | [Self-Correcting](examples/01-self-correcting/) | Reconciler loops, rework queuing, decompose-on-failure | Medium |
| 02 | [Self-Bootstrapping Project](examples/02-self-bootstrapping/) | Full triage → plan → implement → review → merge cycle | Medium |
| 03 | [Design System Building](examples/03-design-system/) | AI-driven UI design reviews creating specs and tasks | Medium |
| 04 | [Media Production Pipeline](examples/04-media-pipeline/) | World → characters → script → art → audio → assembly | Advanced |
| 05 | [Organization Conductor](examples/05-org-conductor/) | Central orchestrator managing 50+ repos with 30+ agents | Advanced |
| 06 | [Multi-Model Routing](examples/06-multi-model/) | Same workflow, different LLMs with fallback chains | Simple |
| 07 | [Quality Gates](examples/07-quality-gates/) | Architecture, security, DevOps, and docs audits on cron | Medium |
| 08 | [Cross-Repo Template Sync](examples/08-cross-repo-sync/) | Keeping multiple framework templates in feature parity | Advanced |
| 09 | [Fleet Management](examples/09-fleet-management/) | Managing multiple AO daemons across repos | Medium |
| 10 | [Knowledge & Decision Pipeline](examples/10-knowledge-pipeline/) | Question generation → action extraction → founder decisions | Advanced |

## How to Use

1. Install [AO CLI](https://github.com/launchapp-dev/ao-cli)
2. Copy any example's `.ao/` directory into your project
3. Customize agents, phases, and schedules for your stack
4. Run with `ao daemon start --autonomous`

## Anatomy of an AO Workflow

```yaml
# Tools the agent is allowed to use
tools_allowlist:
  - git
  - gh
  - npm
  - pnpm

# MCP servers providing additional capabilities
mcp_servers:
  context7:
    command: npx
    args: ["-y", "@upstash/context7-mcp"]

# Agent definitions with system prompts and model assignments
agents:
  implementer:
    system_prompt: |
      You implement code changes...
    model: claude-haiku-4-5
    tool: claude
    mcp_servers: ["ao", "context7"]

# Reusable phase definitions
phases:
  implementation:
    mode: agent
    agent: implementer
    directive: "Implement the task requirements."

  build-check:
    mode: command
    command:
      program: pnpm
      args: ["build"]
      timeout_secs: 300

# Workflows compose phases into pipelines
workflows:
  - id: standard
    name: Standard Task Workflow
    phases:
      - implementation
      - build-check
      - push-branch
      - create-pr
      - pr-review:
          on_verdict:
            rework:
              target: implementation

# Scheduled automation
schedules:
  - id: work-planner
    cron: "*/5 * * * *"
    workflow_ref: work-planner
    enabled: true
```

## Key Concepts

- **Agents** — AI personas with specific system prompts, model assignments, and MCP server access
- **Phases** — Individual steps (either agent-driven or command-based) with directives
- **Workflows** — Ordered sequences of phases, with rework loops and conditional branching
- **Schedules** — Cron-based automation triggers for recurring workflows
- **MCP Servers** — External tool providers (GitHub, Context7, Playwright, etc.)
- **Verdicts** — Review outcomes that can loop back to earlier phases (rework cycles)

## License

MIT
