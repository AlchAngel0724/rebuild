# Rebuild Plan

Goal: rebuild Alchemy Trades as a production-grade local-first desktop app.

Non-negotiables:
- Signing stays on the backend.
- Keys are stored/encrypted locally; no secrets leave the machine.
- “Phone home” is allowed only for opt-in JSON telemetry with strict allowlists.
- No Docker required for baseline install.

Repo structure (monorepo):
- `reference/`: old code/build layouts for reference only.
- `research/`: analysis documents.
- `rebuild/`: new codebase.

Architecture intent (baseline):
- Desktop shell: Electron.
- Local backend: single local service (or Electron main-process service layer) responsible for signing, RPC calls, persistence, and background workers.
- DB: SQLite (WAL) for durable state.
- Queue: SQLite-backed durable job queue.

Milestones:
1. Repo scaffolding + standards docs + CI skeleton.
2. Implement persistence + job queue primitives.
3. Implement signing service + transaction pipeline.
4. Implement grid engine with event-log + snapshots.
5. Implement UI + observability + opt-in telemetry.
