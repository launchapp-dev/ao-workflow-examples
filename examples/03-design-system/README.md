# Design System Building

An AI-driven design review loop where a senior model (Opus) acts as UI/UX Designer, creating detailed design specs and implementation tasks that cheaper models (Haiku/Kimi) then build.

## The Pattern

```
UI Designer (Opus, every 2hrs)
  ↓ reviews pages, creates design specs as requirements
  ↓ creates 2-3 implementation tasks per run
Planner (every 5min)
  ↓ feeds tasks through triage
Implementer (Haiku)
  ↓ builds from design spec
Reviewer (Haiku)
  ↓ merges or requests changes
```

## Why This Works

- **Opus is expensive but strategic** — it only creates specs, never writes code
- **Haiku is cheap and fast** — it implements from detailed specs
- **The shadcn MCP** verifies component availability before creating tasks
- **Max 1 requirement + 3 tasks per run** prevents flooding the queue

## Key Insight

Use your most capable (expensive) model for **decisions** and your fastest (cheapest) model for **execution**. The design review runs every 2 hours, creating a steady stream of polished UI improvements.
