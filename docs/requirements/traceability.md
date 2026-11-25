# Requirement and acceptance traceability

Every source section is covered, including behavioral prose. Section 2 is retained as an external ownership/approval gate in the archive.

| Source section | Contract | Design |
| --- | --- | --- |
| 1. Purpose | [Read](../requirements/product.md) | Cross-component boundary |
| 2. Ownership and program status | [Archive](../source/README.md) | Cross-component boundary |
| 3. End state and core ownership | [Read](../requirements/product.md) | Cross-component boundary |
| 4. Required scope | [Read](../requirements/product.md) | Cross-component boundary |
| 5. Units, numerical domain, and validity | [Read](../requirements/software.md) | [World stepping commands and handle lifetime](../design/world-clock.md) |
| 6. Simulation clock and input semantics | [Read](../requirements/software.md) | [World stepping commands and handle lifetime](../design/world-clock.md) |
| 7. Architecture | [Architecture](../architecture/high-level-design.md) | Cross-component boundary |
| 8. Geometry and mass properties | [Read](../requirements/software.md) | [Geometry validation mass and compound transforms](../design/geometry.md) |
| 9. Broad phase | [Read](../requirements/software.md) | [Sweep-and-prune candidate generation](../design/broad-phase.md) |
| 10. Narrow phase and manifolds | [Read](../requirements/software.md) | [Narrow phase persistent anchors and feature IDs](../design/manifolds.md) |
| 11. Contact solver | [Read](../requirements/software.md) | [Contact impulses friction and correction](../design/solver.md) |
| 12. Joints and mechanical interactions | [Read](../requirements/software.md) | [Distance and revolute constraints motors and islands](../design/joints.md) |
| 13. Continuous collision detection | [Read](../requirements/software.md) | [Restricted circle time-of-impact substeps](../design/ccd.md) |
| 14. Sleeping, determinism, and snapshots | [Read](../requirements/software.md) | [World stepping commands and handle lifetime](../design/world-clock.md) |
| 15. Browser laboratory | [Read](../requirements/browser.md) | Cross-component boundary |
| 16. Scene, API, and data contracts | [Read](../contracts/data-and-artifacts.md) | Cross-component boundary |
| 17. Analytic correctness and tolerances | [Read](../requirements/quality-and-benchmarks.md) | Cross-component boundary |
| 18. Local scale and performance | [Read](../requirements/quality-and-benchmarks.md) | Cross-component boundary |
| 19. Acceptance catalog | [Read](../testing/acceptance-plan.md) | Cross-component boundary |
| 20. Session plan | [Read](../delivery/milestones.md) | Cross-component boundary |
| 21. Stack, deliverables, and risks | [Read](../delivery/milestones.md) | Cross-component boundary |
| 22. Primary technical reference | [Read](../architecture/references.md) | Cross-component boundary |

## Acceptance oracles

| ID | Required evidence | Outcome |
| --- | --- | --- |
| IA-01 | Geometry validation and mass/inertia fixtures pass | NOT RUN |
| IA-02 | Broad phase finds every overlap in 10,000 seeded small scenes | NOT RUN |
| IA-03 | All three mandatory shape-pair combinations produce expected manifolds | NOT RUN |
| IA-04 | Stable feature IDs and warm-start cache invalidation survive contact transitions | NOT RUN |
| IA-05 | Analytic motion, collision, momentum, and energy tests meet stated tolerances | NOT RUN |
| IA-06 | Resting stack and bridge remain within penetration/joint-error bounds | NOT RUN |
| IA-07 | Friction impulses satisfy the Coulomb bound and oppose tangential motion | NOT RUN |
| IA-08 | Revolute limits and motor torque caps are enforced | NOT RUN |
| IA-09 | Sleep and wake behavior works through contacts, joints, and external impulses | NOT RUN |
| IA-10 | CCD launch/grazing fixtures pass; unsupported CCD pairs remain clearly labeled | NOT RUN |
| IA-11 | CCD limit reports a failed/incomplete run instead of tunneling silently | NOT RUN |
| IA-12 | Same-build repeated runs and snapshot continuation have identical digests | NOT RUN |
| IA-13 | Destroy/recreate cycles cannot use stale body or joint handles | NOT RUN |
| IA-14 | Malformed/corrupt/incompatible scenes and snapshots fail explicitly | NOT RUN |
| IA-15 | Mandatory tick-time and memory bars pass with fixed settings | NOT RUN |
| IA-16 | Soak has zero numerical failures and bounded object/contact retention | NOT RUN |
| IA-17 | Browser tests cover load, inspect, impulse, pause, step, snapshot, and restore | NOT RUN |
| IA-18 | Simulation remains functional with software rendering and no sound | NOT RUN |
| IA-19 | Numerical failure report identifies a reproducible scene, tick, and pair/joint | NOT RUN |
| IA-20 | Fresh local commands reproduce all mandatory fixtures and reports offline | NOT RUN |
