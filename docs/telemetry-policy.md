# Telemetry Policy (Opt-in)

Telemetry is allowed only when explicitly enabled by the user.

Hard rules:
- JSON-only payloads.
- Allowlist fields only.
- No Web3 secrets: never send private keys, seed phrases, decrypted key material, wallet export data, raw signed tx bytes, or anything that could reconstruct them.

Recommended allowlist examples:
- app version, OS version
- feature flags enabled
- counts (number of grids), anonymized performance aggregates
- error codes / stack traces with redaction

User controls:
- Toggle on/off
- View last payload
- Export telemetry data
- Delete telemetry data
