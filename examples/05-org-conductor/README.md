# Organization Conductor

A central orchestrator that manages 50+ repositories through a scan → compare → dispatch loop. Runs every 20 minutes, coordinating 30+ specialized agents.

## The Cycle

Every 20 minutes:

1. **SCAN** — What changed across the org?
   - Recent commits, new issues, open PRs
   - AO task list and queue status

2. **COMPARE** — Is knowledge stale?
   - Product docs vs actual repo activity
   - Architecture diagrams vs code structure
   - Competitive info freshness

3. **DISPATCH** — Queue the right work
   - Strict deduplication (never create duplicate tasks)
   - Rate limiting (max 1-3 tasks per cycle)
   - Priority ordering

4. **UNBLOCK** — Fix stuck tasks
   - Re-enqueue tasks stuck in 'ready' > 1 hour
   - Decompose tasks that failed 3+ times
   - **Never cancel** — always decompose

## Agents Dispatched

The conductor doesn't do the work — it dispatches to specialists:

| Agent | Trigger |
|-------|---------|
| Product Cataloger | New repo appeared or docs stale > 7 days |
| Knowledge Curator | Significant commits that knowledge doesn't reflect |
| Architecture Diagrammer | Code structure changed, diagrams > 14 days old |
| Competitive Researcher | Competitor info > 14 days old |
| SDK Auditor | SDK versions changed |
| Template Syncer | Template repo merged PR that others don't have |
| Quality Runner | Repo had > 5 PRs merged in 7 days |
| Fleet Manager | Daemon crashed or repo needs AO setup |

## Key Insight

The conductor is a **meta-agent** — it doesn't produce artifacts, it ensures the right work happens at the right time. Think of it as a project manager that never sleeps.
