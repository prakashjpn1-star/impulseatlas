# Scene snapshot and report formats

## Scene and numerical contract

Scene JSON is version 1 and validated by [scene schema](../schemas/scene.schema.json). Units are m, kg, s and rad; core scalars are IEEE-754 binary64. Proposed fixture-size interpretation is outer local bounding extent 0.05–10 m (circle radius 0.025–5 m); the semantic importer checks transformed world domain and computed dynamic mass.

Commands have unique order within each target tick. Settings, generated seed, engine build and scene content identify a run. Finite JSON syntax alone does not validate convexity, normals or positive inertia.

## Tick ordering

Apply commands, integrate forces into velocity, update proxies/manifolds, warm start, solve velocity constraints, integrate positions (restricted bullets use TOI substeps instead), refresh geometry, solve bounded positional constraints, update sleep, check finite state, then publish a completed tick. No bullet gets a second full-dt position integration.

Proposed tolerances are 0.005 m contact slop, 0.2 m maximum position correction per iteration, 1e-6 m minimum accepted geometric edge, 1e-10 m² degeneracy threshold and two-degree angular limit slop. These quantities have different units/purposes. The fixed benchmark manifest records them; no unexplained universal epsilon is substituted.

## Snapshot

Use magic IASN, little-endian u32 format version, u64 tick and bounded section lengths, followed by build/config/scene identity, body/fixture/joint state, handle slots/generations, sleep counters, persistent contact features and impulses, pending commands and payload SHA-256. Store binary64 bit patterns in declared order; nonfinite state is rejected and negative-zero normalization is explicitly consistent.

Section lengths/counts are verified before allocation. A snapshot is selected only after complete checksum/structure validation. Derived broad-phase data may be reconstructed only with unchanged canonical processing order. Same-build continuation is compared for 10,000 ticks; cross-compiler/CPU identity is not promised.

## Reports

Retain exact scene/config/build, tick range, awake/contact/CCD work, timing distribution, physics-versus-render time, memory, oracle tolerances and failure location. No actual checksums or passing results are invented in these examples.
