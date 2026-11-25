# Offline setup operation and artifact recovery

The reference stack is: C++20 with double-precision scalar CPU math, a small permitted local HTTP adapter, and HTML/CSS/JavaScript with Canvas 2D or SVG. Compiler/library availability remains an environment gate. No existing physics engine supplies the core.

Inventory the actual permitted compiler/runtime and mirror before pinning versions; record license notices and offline build/test commands. Runtime CLIs are implementation deliverables, not existing executable engines in this documentation baseline. Headless tests must not require a browser or sound/GPU path.

Keep source, generated fixtures, runtime staging and immutable evidence in separate directories. Format changes reject incompatible artifacts clearly. Before selecting new artifacts, complete/verify them and preserve a valid previous selection. Restore into an isolated run/project directory rather than silently editing current state.

Restore includes tick, commands, caches/sleep/handle generations and exact build/config. Stop conditions retain failed tick diagnostics; never skip ticks to make real-time playback look recovered.

Back up immutable inputs/artifacts/manifests and raw reports together with checksums. A checkpoint/snapshot cannot recover later changes absent from it. Cleanup preserves active artifacts and failure evidence. Process-stop recovery claims do not imply arbitrary power-loss or corrupted-disk recovery.
