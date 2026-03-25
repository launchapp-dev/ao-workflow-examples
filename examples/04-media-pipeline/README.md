# Media Production Pipeline

A full creative production pipeline that generates serialized comic/animated content — from world-building through final QA. Each agent is a specialist with database-enforced constraints ensuring narrative coherence.

## The Pipeline

```
World Building (one-time)
  ├── create-world → locations, rules, systems
  ├── create-characters → profiles, relationships, voice styles
  └── plan-season → arcs, plot beats, foreshadowing

Episode Production (per episode)
  ├── outline-episode → scene-by-scene outline
  ├── write-script → panel-by-panel with dialogue, camera, mood
  ├── script-review → continuity, voice, pacing checks
  ├── art-direction → image prompts for each panel
  ├── generate-images → AI image generation
  ├── generate-audio → dialogue, music, SFX
  ├── assemble-episode → compositing + layout
  └── quality-check → final QA before human review
```

## What Makes This Special

### MCP-Enforced Validation
The storyforge MCP server **rejects invalid writes**:
- Character references something not in their `knowledge_state` → rejected
- Scene contradicts established world rules → rejected
- Dead character assigned dialogue → rejected
- Dialogue doesn't match character's `voice_style` → rejected

### Genre-Specialized Writers
Different LLMs handle different genres:
- **Claude Opus** — horror (deep psychology required)
- **Claude Sonnet** — comedy, general episodes
- **Gemini** — action sequences

### Database-Centric Architecture
```
PostgreSQL (universe truth)
    ↓
storyforge MCP (validates reads/writes)
    ↓
AO Agent Orchestration (phases in sequence)
    ↓
replicate MCP (image generation)
    ↓
audio MCP (voice + music + SFX)
    ↓
assembly MCP (panel compositing)
    ↓
review MCP (human review queue)
```

## Key Insight

By putting the "source of truth" in a database with MCP-enforced validation, you can have multiple AI agents collaborating on creative work while maintaining consistency. The database is the guardrail — not the agents' memory.
