# Fleet Management

Manage multiple AO daemon instances across an organization. Set up new repos, start/stop daemons, monitor health, scale pool sizes, and handle deployments.

## Capabilities

1. **Setup AO in a repo** — Clone, configure, create workflows tailored to the tech stack
2. **Start/Stop daemons** — Launch autonomous agents with configurable pool sizes
3. **Monitor health** — Check all running daemons, restart crashed ones
4. **Scale pools** — Increase for large backlogs, decrease for empty queues
5. **Deploy** — Vercel for frontends, Railway for backends

## Key Insight

A fleet manager turns a collection of independent repos into a coordinated workforce. When a repo accumulates a backlog, the fleet manager can spin up more workers. When a daemon crashes, it auto-restarts. This is infrastructure-as-code for AI agents.
