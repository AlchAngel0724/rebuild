# Queue / Worker Standards (No External Broker)

Default: SQLite-backed durable job queue.

## Why
- No Docker assumption.
- Durable across crashes/reboots.
- Keeps signing and RPC submission off the UI/request path.

## Job lifecycle
- `queued` -> `running` -> `succeeded` | `failed` -> retry -> `dead`.

## Claiming model (lease)
- Workers claim jobs via an atomic update inside a transaction.
- Use `locked_by` + `locked_until` lease fields to prevent double processing.

## Retries
- Exponential backoff with jitter.
- Cap retries; move to `dead` with last error captured.

## Idempotency
- Every external side effect job (e.g., broadcast tx) must have an idempotency key.
- On retry, the worker must detect if the effect already happened.

## Worker placement
- Default: Electron main process spawns a worker pool (worker threads) for background jobs.
- Optional: separate worker process if isolation is required.
