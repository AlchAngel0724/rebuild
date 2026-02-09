# SQLite Standards (Local-First)

SQLite is the default local database for the rebuild.

## Key design goal
Support many concurrent grids without writing on every price tick.

## Required configuration
- WAL mode enabled.
- `busy_timeout` configured (avoid spurious “database is locked”).
- Use explicit transactions; batch related writes.

## Concurrency model
- Single-writer principle: serialize writes through a single DB worker (thread/process) or a single shared write-queue.
- Many readers are allowed; WAL supports concurrent reads while writes occur.

## Write policy
Never write on price tick.

Only write on meaningful events:
- order placed
- order filled
- tx submitted / confirmed / failed
- grid parameters changed
- grid shifted (levels moved)

## Event-log + snapshot pattern (recommended)
- Hot state in memory for decision-making.
- Persist an append-only event record for every trade/grid move.
- Periodically checkpoint (snapshot) compact current grid state.

Rationale: avoid rewriting large “levels tables” on every shift.

## Schema guidelines
- `grid_state`: one row per grid with the current derived state.
- `trade_events`: append-only trade/tx events.
- `grid_events`: append-only grid changes (shift, resize, pause/resume).
- Index `(grid_id, created_at)` on event tables.

## Idempotency
- All “submit tx / record fill” operations must support idempotency keys.
- Store idempotency key with unique constraint to prevent duplicates.
