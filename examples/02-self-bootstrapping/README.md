# Self-Bootstrapping Project

A complete autonomous development cycle: a Product Owner creates tasks, a Planner feeds them into triage, a Triager routes to the right implementation workflow, and agents build, test, review, and merge — all without human intervention.

## The Loop

```
Product Owner (every 30min)
  ↓ creates tasks
Planner (every 5min)
  ↓ enqueues tasks through triage
Triager
  ↓ validates + routes to workflow
Implementer
  ↓ writes code + commits
Build/Lint/Push/PR
  ↓
Reviewer
  ↓ merges or requests changes
Reconciler (every 10min)
  ↓ unblocks, promotes, heals state
```

## Agents

| Agent | Model | Role |
|-------|-------|------|
| Product Owner | claude-opus-4-6 | Strategic: evaluates features, creates tasks |
| Planner | claude-haiku-4-5 | Tactical: feeds ready tasks into triage pipeline |
| Triager | claude-haiku-4-5 | Routes tasks by complexity/type to right workflow |
| Decomposer | claude-sonnet-4-6 | Breaks complex tasks into 2-4 subtasks |
| Implementer | claude-haiku-4-5 | Writes code, runs build, commits |
| Reviewer | claude-haiku-4-5 | Reviews PRs, merges or requests changes |
| Reconciler | claude-haiku-4-5 | Heals task state, unblocks dependencies |

## Key Insight

The system is self-sustaining: the Product Owner continuously creates work, the Planner feeds it into the pipeline, and the Reconciler ensures nothing gets stuck. This runs 24/7 without human intervention, producing real PRs.
