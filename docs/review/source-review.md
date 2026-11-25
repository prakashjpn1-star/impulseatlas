# Review findings and design boundaries

| Risk | Design response |
| --- | --- |
| Missed broad-phase pairs | Compare every eligible overlap with an independent brute-force small-scene oracle. |
| Stale warm-start impulses | Match persistent feature IDs and fixture generations; clear mismatched caches. |
| Energy injected by correction | Bound position correction and report residual/energy with the correct fixture assumptions. |
| Overbroad CCD claim | Only bullet circles versus supported static shapes have the mandatory continuous path. |

The reference stack and algorithms are concrete design proposals; exact toolchain versions and quantitative results remain open evidence gates. Required core ownership and independent oracles are preserved. CCD remains restricted and determinism remains same-build.

Ownership/approval clauses are preserved in the source archive. Active documents explain technical contracts rather than instructing someone to write submission answers. AI assistance remains disclosed; no programme approval or participant-authored statement is implied.
