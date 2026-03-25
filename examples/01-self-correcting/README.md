# Self-Correcting Workflows

Workflows that detect failures and automatically recover — through rework loops, task decomposition, and state reconciliation.

## Patterns

### 1. Rework Loop
When a PR reviewer finds issues, the workflow loops back to implementation automatically:

```
implement → push → create-pr → review
                                  ↓ (changes requested)
                              rework → force-push → review (again)
```

### 2. Decompose on Failure
When a task fails 3+ times, instead of giving up, it's broken into smaller subtasks:

```
task fails 3x → decomposer agent → 2-4 subtasks → each runs independently
```

### 3. Rebase and Retry
When a PR has merge conflicts, automatically rebase and re-review:

```
conflicting PR → rebase on main → force push → re-review
```

### 4. Task Reconciler
A cron-based agent that continuously heals task state:
- Unblocks tasks whose dependencies are met
- Promotes backlog items to ready
- Re-routes failed workflows to decompose
- Marks tasks with merged PRs as done
- **Never cancels** — always decomposes instead

## Key Insight

The self-correcting pattern means the system **never gives up**. Failed tasks get decomposed into simpler pieces. Conflicting PRs get rebased. Stale state gets reconciled. This creates a resilient system that can run autonomously for weeks.
