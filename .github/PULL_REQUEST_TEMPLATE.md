## What changed

## Why

## Checklist
- [ ] No secrets committed (.env, private keys, seed phrases)
- [ ] No logging of sensitive data (keys, decrypted material, raw tx bytes)
- [ ] Local-first: no new mandatory external services (Docker optional only)
- [ ] SQLite standards followed (WAL + batched writes; no tick writes)
- [ ] Jobs use idempotency + retries where applicable
- [ ] Documentation updated (`docs/decisions.md` / relevant standards)
