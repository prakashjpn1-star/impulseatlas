# Accuracy resources and performance requirements

These pass bars are required targets, not measured results. Accuracy, resource and performance evidence use frozen fixtures/settings.

## Analytic correctness and tolerances

Use independent checks rather than treating another engine's trajectory as exact truth. Required fixtures include constant-velocity motion, discrete free fall, circle collision, rest on a flat static box, sliding friction, pendulum/joint length, and CCD time of impact.

For free fall with no contacts, compare against the closed-form semi-implicit recurrence to 1e-8 m over 60 ticks. Also compare with continuous motion and verify that halving timestep approximately halves first-order position error, within a declared 10% ratio tolerance away from roundoff.

For isolated equal-mass elastic head-on circles with gravity/friction disabled, final velocities match analytic values within 1e-3 m/s, momentum relative error is at most 1e-6, and kinetic-energy relative error is at most 1%. Energy conservation is not required in inelastic, frictional, powered, or kinematically driven scenes.

For the fixed bridge/pendulum fixtures, joint-length error is at most 0.02 m after 2,000 ticks. A ten-box resting stack must remain bounded for 10,000 ticks, with maximum penetration at most 0.02 m after settling. Freeze the exact fixture dimensions, iterations, and settling period before acceptance.

## Local scale and performance

| Workload | Proposed pass bar |
| --- | --- |
| Real-time scene | 1,000 awake dynamic circles/boxes, at most 2,000 persistent contact points, fixed 60 Hz configuration |
| Tick cost | p95 headless physics time at most 16.7 ms over 3,600 measured ticks after 600 warm-up ticks |
| Small-scene geometry campaign | 10,000 seeded scenes of at most 100 fixtures; broad phase misses zero eligible overlaps |
| CCD campaign | 1,000 supported fast-circle launches; zero tunneling and correct miss classification |
| Mechanical suite | Four required compound scenes, including ten-link bridge and motor interaction |
| Determinism | Twenty repeated runs and snapshot continuations produce matching same-build digests |
| Memory | At most 512 MiB application memory for the mandatory 1,000-body scene, excluding browser/OS |
| Soak | 30 minutes of simulated stepping with controlled create/destroy cycles; zero nonfinite states or unbounded retained handles |

These are proposed thresholds, not results. Report hardware, runtime, precision, iterations, awake bodies, actual contacts, CCD work, memory, and the entire timing distribution. Rendering cost is measured separately and never substituted for physics cost. A 5,000-body scene is a stretch benchmark with an honest reported result, not a required real-time promise.
