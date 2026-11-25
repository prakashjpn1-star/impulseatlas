# Delivery and release gate

Deliver runnable slices with actual evidence and explicit remaining failures; required quantitative bars remain intact.

## Session plan

1. Freeze units, validity limits, timestep, tolerances, and analytic fixtures.
2. Implement geometry, mass properties, body integration, and headless stepping.
3. Build broad phase and independent overlap comparisons.
4. Implement manifolds, feature persistence, and geometry edge cases.
5. Build normal/friction impulse solver, warm starting, and resting-stack tests.
6. Add distance/revolute joints, limits, motors, and compound mechanical scenes.
7. Add restricted CCD, sleeping, deterministic ordering, and snapshot continuation.
8. Build browser laboratory and numerical overlays.
9. Run performance campaigns and soak; diagnose solver errors without weakening tests.
10. Complete offline reproduction, evidence review, and documented limitations.

Each session retains runnable fixtures, actual tests and failures, and its next checkpoint. The project spans multiple days and uses the program's separate session time rules.

## Stack, deliverables, and risks



Deliver source, numerical-method notes, scene specification, generated fixtures, headless CLI, UI, analytic oracle tests, profile/benchmark runner, raw reports, and acceptance matrix. Preserve failing scenes and exact configuration rather than replacing evidence with a successful-looking template.

The main risks are unstable contact correction, inconsistent normals, missed broad-phase pairs, stale cached impulses, and an overly broad CCD promise. A bounded supported domain and explicit tolerances make these risks testable. Expansion to 3D or soft bodies follows only after the required core passes.
