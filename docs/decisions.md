# Decisions

This file tracks decisions and open questions.

## Decided
- Monorepo.
- Desktop shell: Electron.
- Windows distribution: signed installer.
- Local DB: SQLite.
- Broker/queue: SQLite job queue (no Docker requirement).
- Telemetry: opt-in minimal.

## Open
- Backend runtime choice:
  - Option A: Node.js + TypeScript (aligns with Electron; strongest monorepo tooling; shared types).
  - Option B: Python (strong for analytics; packaging complexity increases in Electron context).
  - Option C: Hybrid (Node app shell + Python strategy modules).

Evaluation criteria:
- Packaging complexity (single installer)
- AV false positives
- Signing throughput vs RPC latency (signing usually not the bottleneck)
- Maintainability + type safety
