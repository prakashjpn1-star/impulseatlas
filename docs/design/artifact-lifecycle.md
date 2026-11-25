# Artifact storage identity and publication

```mermaid
erDiagram
    WORLD ||--o{ BODY : owns
    BODY ||--|{ FIXTURE : compounds
    FIXTURE ||--o{ CONTACT_POINT : touches
    WORLD ||--o{ JOINT : constrains
    WORLD ||--o{ TICK_COMMAND : orders
    SNAPSHOT ||--o{ HANDLE_GENERATION : retains
    SNAPSHOT ||--o{ WARM_CACHE : preserves
    RUN_REPORT ||--o{ TICK_SAMPLE : measures
```

The [format specification](../../formats/README.md) defines versioning, provenance and checksums. These projects need immutable files/owned memory, not an invented mandatory database.

Build a new artifact in a controlled staging location, complete its payload, close/flush using documented host guarantees, verify checksums/structure and atomically select it through a small manifest or supported same-filesystem rename. Record what is and is not guaranteed under process stop versus power loss. Partial files never replace a valid selected artifact.

Snapshot selection is at a completed tick boundary and retains warm caches, handle generations, sleep and pending commands. Restore creates a new run with explicit parent provenance.

Malformed versions, truncated payloads, path escapes and inconsistent identities are explicit errors. Cleanup has finite retained-count/byte limits and preserves active/pinned artifacts and raw failure reports. No regeneration command overwrites executed evidence.
