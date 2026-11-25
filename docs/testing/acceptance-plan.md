# Acceptance and oracle plan

Independent oracles and preserved counterexamples establish correctness. Every acceptance item starts NOT RUN.

## Analytic correctness and tolerances

Use independent checks rather than treating another engine's trajectory as exact truth. Required fixtures include constant-velocity motion, discrete free fall, circle collision, rest on a flat static box, sliding friction, pendulum/joint length, and CCD time of impact.

For free fall with no contacts, compare against the closed-form semi-implicit recurrence to 1e-8 m over 60 ticks. Also compare with continuous motion and verify that halving timestep approximately halves first-order position error, within a declared 10% ratio tolerance away from roundoff.

For isolated equal-mass elastic head-on circles with gravity/friction disabled, final velocities match analytic values within 1e-3 m/s, momentum relative error is at most 1e-6, and kinetic-energy relative error is at most 1%. Energy conservation is not required in inelastic, frictional, powered, or kinematically driven scenes.

For the fixed bridge/pendulum fixtures, joint-length error is at most 0.02 m after 2,000 ticks. A ten-box resting stack must remain bounded for 10,000 ticks, with maximum penetration at most 0.02 m after settling. Freeze the exact fixture dimensions, iterations, and settling period before acceptance.

## Acceptance catalog

All items start **NOT RUN**.

| ID | Required evidence |
| --- | --- |
| IA-01 | Geometry validation and mass/inertia fixtures pass |
| IA-02 | Broad phase finds every overlap in 10,000 seeded small scenes |
| IA-03 | All three mandatory shape-pair combinations produce expected manifolds |
| IA-04 | Stable feature IDs and warm-start cache invalidation survive contact transitions |
| IA-05 | Analytic motion, collision, momentum, and energy tests meet stated tolerances |
| IA-06 | Resting stack and bridge remain within penetration/joint-error bounds |
| IA-07 | Friction impulses satisfy the Coulomb bound and oppose tangential motion |
| IA-08 | Revolute limits and motor torque caps are enforced |
| IA-09 | Sleep and wake behavior works through contacts, joints, and external impulses |
| IA-10 | CCD launch/grazing fixtures pass; unsupported CCD pairs remain clearly labeled |
| IA-11 | CCD limit reports a failed/incomplete run instead of tunneling silently |
| IA-12 | Same-build repeated runs and snapshot continuation have identical digests |
| IA-13 | Destroy/recreate cycles cannot use stale body or joint handles |
| IA-14 | Malformed/corrupt/incompatible scenes and snapshots fail explicitly |
| IA-15 | Mandatory tick-time and memory bars pass with fixed settings |
| IA-16 | Soak has zero numerical failures and bounded object/contact retention |
| IA-17 | Browser tests cover load, inspect, impulse, pause, step, snapshot, and restore |
| IA-18 | Simulation remains functional with software rendering and no sound |
| IA-19 | Numerical failure report identifies a reproducible scene, tick, and pair/joint |
| IA-20 | Fresh local commands reproduce all mandatory fixtures and reports offline |
