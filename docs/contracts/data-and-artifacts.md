# Data and artifact contracts

Immutable input/build/configuration identity connects artifacts, results and recovery.

## Scene, API, and data contracts

Versioned JSON scenes contain world settings, materials, body/fixture definitions, joints, and deterministic command scripts. A run retains the scene hash, configuration hash, engine build, seed, commands, snapshots, and measurements.

The local API supports create world, load scene, submit tick commands, advance N ticks, pause/run, inspect bounded state, inspect contacts/joints, save/restore snapshot, run a named test, and retrieve a report. Suggested routes are `/worlds`, `/worlds/{id}/commands`, `/worlds/{id}/steps`, `/worlds/{id}/state`, `/worlds/{id}/snapshots`, and `/reports`.

Bound body count, fixtures per body, joint count, command backlog, ticks per request, snapshot bytes, and diagnostic history. Return structured validation, stale-handle, numerical-failure, resource-limit, and stopped-run errors. The service binds to loopback and controls no external process or system.
