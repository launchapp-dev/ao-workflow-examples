# Multi-Model Routing

The same workflow definition can route to different LLMs, with fallback chains for resilience. This lets you optimize cost, speed, and quality per task type.

## The Pattern

Define the same workflow multiple times, each using a different model:

```yaml
workflows:
  - id: standard           # Default (Claude Haiku — fast, cheap)
  - id: standard-gemini    # Gemini variant
  - id: standard-kimi      # Kimi variant
  - id: standard-minimax   # MiniMax variant
```

The **triager** routes tasks to the right variant based on complexity:

| Complexity | Type    | Model         |
|------------|---------|---------------|
| low        | any     | Kimi (cheapest) |
| medium     | feature | Claude Haiku  |
| medium     | bugfix  | Claude Haiku  |
| high       | any     | Claude Sonnet |
| critical   | any     | Claude Opus   |

## Fallback Chains

Each model has fallback options if the primary is rate-limited or unavailable:

```yaml
runtime:
  fallback_models:
    - gpt-4.1
    - claude-haiku-4-5
```

## Key Insight

Not every task needs your most expensive model. Simple tasks (rename a variable, fix a typo, add a dependency) can use the cheapest model available. Complex architectural changes get routed to Opus. This can reduce costs by 10x while maintaining quality where it matters.
