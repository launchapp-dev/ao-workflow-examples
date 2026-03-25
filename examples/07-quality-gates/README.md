# Quality Gates

Scheduled audit workflows that continuously verify project health — architecture integrity, security, DevOps readiness, and documentation sync. Each runs on a cron schedule and creates tasks for issues found.

## Audits

| Audit | Frequency | What It Checks |
|-------|-----------|----------------|
| QA & Security | Every 2 hours | Build, lint, type safety, hardcoded secrets, auth security, injection vectors |
| Architecture | Every 3 hours | Dependency graph, circular deps, package boundaries, Dockerfile, CI/CD |
| Documentation | Every 3 hours | CLAUDE.md, .env.example, README, route docs, export surfaces |
| DevOps | Every 6 hours | Dockerfile, infrastructure scripts, CI/CD readiness |
| Smoke Test | Every hour | Dev server starts, pages load via Playwright |
| Research | Every hour | Package updates, new integrations, best practices |

## Key Insight

Quality is not a one-time check — it's a continuous loop. Every 2-3 hours, specialized agents verify the project is healthy and create tasks for anything that drifted. This catches regressions fast, before they compound.
