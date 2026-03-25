# Cross-Repo Template Sync

Keep multiple framework variants of the same product in feature parity. When the flagship template gets a new feature, it's automatically ported to all other variants.

## The Problem

You have the same SaaS template in 4 frameworks:
- React Router (flagship)
- Next.js
- Nuxt
- SvelteKit

Some packages are **shared** (auth, billing, database — identical TypeScript). Others are **framework-specific** (UI components, routing — must be ported, not copied).

## The Solution

A sync agent runs every 3 hours, comparing all templates:

1. **Package Diff** — For each shared package, find the most complete version and sync to others
2. **Feature Parity** — Compare routes; create tasks to port missing features
3. **Dependency Sync** — If one upgraded a shared dep, create tasks for others to match
4. **Config Sync** — biome.json, turbo.json, tsconfig — sync improvements

## Rules

- **Shared packages**: copy files directly (same TypeScript)
- **Framework-specific (apps/web, ui-kit)**: PORT features, never copy
- Always create PRs, never push to main
- Max 5 PRs per run to avoid flooding

## Key Insight

Cross-repo sync transforms a single improvement into organization-wide uplift. One team's work benefits all variants automatically.
