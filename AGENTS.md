# Agent Rules (Alchemy Trades Rebuild)

This repository is a local-first trading application rebuild.

Hard constraints:
- Private keys never leave the local machine.
- Do not print/log private keys, seed phrases, raw decrypted key material, or wallet export data.
- “Phone home” telemetry is opt-in and must be JSON-only, allowlisted, and must never include Web3 secrets.
- Default assumption: no Docker on end-user machines.

Working conventions:
- `reference/` is read-only historical baseline (do not modify unless explicitly asked).
- `research/` is research artifacts (analysis, notes, comparisons).
- `rebuild/` is the new implementation workspace.

Engineering standards:
- Prefer smallest viable change; avoid refactors while fixing bugs.
- Prefer deterministic behavior: idempotency keys, retries with backoff, explicit timeouts.
- For local data: prefer SQLite in WAL mode + migrations.
- For background work: prefer a SQLite-backed job queue + worker pool (no external broker by default).

Documentation-first:
- Before implementation, update/confirm `docs/decisions.md` and the relevant standards docs.
