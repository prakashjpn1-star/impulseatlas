# API contract

The local API validates bounded input, pins exact run/artifact identity and distinguishes domain failures from infrastructure faults.

## Scene, API, and data contracts

Versioned JSON scenes contain world settings, materials, body/fixture definitions, joints, and deterministic command scripts. A run retains the scene hash, configuration hash, engine build, seed, commands, snapshots, and measurements.

The local API supports create world, load scene, submit tick commands, advance N ticks, pause/run, inspect bounded state, inspect contacts/joints, save/restore snapshot, run a named test, and retrieve a report. Suggested routes are `/worlds`, `/worlds/{id}/commands`, `/worlds/{id}/steps`, `/worlds/{id}/state`, `/worlds/{id}/snapshots`, and `/reports`.

Bound body count, fixtures per body, joint count, command backlog, ticks per request, snapshot bytes, and diagnostic history. Return structured validation, stale-handle, numerical-failure, resource-limit, and stopped-run errors. The service binds to loopback and controls no external process or system.

## Concrete companion contracts

[JSON Schemas](../../schemas/README.md), [worked examples](../../examples/README.md) and [artifact formats](../../formats/README.md) define proposed shapes. Validation errors are 400/422, missing targets 404, stale identity/revision 409, excessive bytes 413 and resource/unavailable conditions explicit 429/503 or typed domain errors as appropriate. Responses carry stable code/message, correlation ID and exact run/artifact identity. Numerical, NO_ROUTE, compile rejection, guest trap and internal fault remain distinct domain outcomes, not flattened into generic success. Default inspection pages are 50, maximum 200 unless a stricter domain limit applies.
