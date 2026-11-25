# Software and domain requirements

Fixed physics ticks and stable constraint ordering determine state. Rendering is separate. Same-build determinism is required; cross-platform bitwise identity and real-world material accuracy are not claimed.

## Units, numerical domain, and validity

Use meters, kilograms, seconds, radians, and double-precision floating point. The supported scene domain is a 200 m by 200 m region, fixture sizes from 0.05 m to 10 m, masses from 0.1 kg to 1,000 kg, and ordinary speeds up to 50 m/s. Explicit bullet fixtures may reach 150 m/s in CCD tests.

Validate finite coordinates, positive mass/density, nonnegative friction, restitution in [0,1], convexity, vertex order, area, and joint parameters. Reject self-intersections, degenerate polygons, and invalid inertia. Define one documented tolerance policy with units; do not use an unexplained epsilon everywhere.

The benchmark settings are fixed before measurement. Do not silently reduce iterations, clamp velocities, remove bodies, or disable contacts to make a difficult scene meet a timing bar. If a resource/numerical limit is reached, report the limit and mark the run failed or incomplete.

## Simulation clock and input semantics

The reference configuration advances at a fixed timestep of 1/60 second. Use semi-implicit Euler for unconstrained integration: update velocity from forces, then advance positions using the new velocity, within the documented contact/constraint step ordering.

Wall-clock rendering does not determine physics timestep. The browser may interpolate for display, but interpolated state is never fed back into simulation. A slow machine may run behind real time; it must not skip physics ticks silently.

Every mutation command has a target tick and stable command order. Commands include create/destroy body, set kinematic motion, apply force, apply impulse, create/destroy joint, and change supported material parameters. Apply them at tick boundaries. Reject commands for completed ticks unless the user explicitly restores an earlier snapshot and starts a new run.

## Geometry and mass properties

Compute area, center of mass, mass, and inertia for circles and convex polygons; combine compound fixtures using the parallel-axis theorem. External body transforms describe the body frame, while dynamics advance its center of mass consistently.

Implement point containment, AABB calculation, segment/ray queries, and shape overlap queries with documented boundary behavior. Normals must have consistent direction. Coincident circle centers and nearly parallel edges require deterministic fallback rules rather than division by zero.

Use hand-calculated shapes and transformed copies as fixtures. Rotation/translation of a valid shape should preserve mass and inertia about its own center. Geometry validation cannot depend on whichever order a hash map returns vertices.

## Broad phase

Implement a dynamic AABB tree or sweep-and-prune structure, with a documented update policy. Maintain stable body/fixture IDs. Emit each candidate pair once, apply collision filters, and process pairs in canonical ID order.

For small random scenes, compare candidates with an independent brute-force pair checker: every truly overlapping eligible pair must appear among candidates. Extra candidates are permitted and counted. Report tree quality or sweep work, candidate count, actual contacts, and update cost.

Moving, destroying, waking, or teleporting a body must update the broad phase correctly. Recycled handles carry generations so a deleted body cannot be confused with a newly allocated one.

## Narrow phase and manifolds

Required shape combinations are circle/circle, circle/polygon, and polygon/polygon. A separating-axis and clipping implementation is suitable for convex polygons; choose and document the actual algorithm.

Produce contact normals, separation/penetration, local anchors, and persistent feature identifiers. Polygon contacts support up to two points. Contact identity survives ordinary small motion so warm starting is meaningful; invalidated features cannot retain unrelated impulses.

Specify collision skin/slop, touch-versus-overlap behavior, and normal orientation. Tests cover edge contact, vertex contact, nearly parallel faces, containment, duplicate points rejected at import, and transitions between manifold types.

## Contact solver

Implement an iterative sequential-impulse solver with accumulated normal and friction impulses, warm starting, rotational effects, restitution, and bounded positional correction. Normal impulses cannot attract separating bodies. Tangential impulse magnitude is bounded by the chosen friction coefficient times accumulated normal impulse.

Use geometric-mean friction mixing and maximum restitution mixing for the first release. Disable restitution below a documented 1 m/s normal approach threshold to reduce resting jitter. Record these policies in scene metadata.

Use stable constraint ordering and fixed iteration counts for deterministic baseline runs. Expose velocity and position iterations, warm-starting mode, residuals, and penetration statistics. Position correction must not inject unbounded energy. Any numerical failure identifies the tick, body pair/joint, and nonfinite value.

## Joints and mechanical interactions

Implement distance joints with a fixed rest length and revolute joints with anchor constraints, optional angular limits, and optional motor target speed/max torque. Enforce motor limits through accumulated impulses rather than unbounded corrective forces.

Reject singular configurations that cannot be solved under the supported model, such as a meaningful movable constraint between two immovable bodies. Define whether connected bodies collide. Waking one body through an applied impulse or motor change must wake the connected active island as needed.

Required compound scenes include a pendulum, a hinged bridge with ten links, a motor-driven crank, and a stack interacting with a moving kinematic platform. These exercise solver coupling beyond isolated demonstration objects.

## Continuous collision detection

The mandatory CCD scope is a moving circle against static axis-aligned boxes and static circles. Ordinary polygon motion remains discrete and is labeled accordingly. Do not imply that every shape pair has CCD.

Compute time of impact over the remaining tick, advance to the earliest valid impact, resolve contact, and process the remaining time with a bounded event count. Handle grazing corners, initially touching/separating shapes, and simultaneous impacts with stable tie-breaking.

If more than eight CCD impacts are required in a tick, return an explicit `CCD_LIMIT` diagnostic and stop that run instead of letting the object pass through a wall. Test 1,000 generated launches at up to 150 m/s against walls as thin as 0.05 m. Report zero tunneling for this supported fixture family and expected no-impact results for grazing misses.

## Sleeping, determinism, and snapshots

Sleeping uses fixed velocity thresholds and tick counts, not wall time. Bodies wake on meaningful contact, joint interaction, impulses, or fixture changes. A sleeping body still participates in relevant overlap queries and can be awakened correctly.

Require identical state digests for repeated runs using the same executable/runtime, configuration, scene, and command sequence. Do not claim bitwise determinism across compilers, CPU architectures, or runtimes. Stable pair/constraint ordering and seeded randomness are mandatory.

A snapshot includes tick, body/joint state, sleep counters, persistent contact/warm-start caches, handle generations, configuration, and pending commands. Restore must reproduce uninterrupted execution for 10,000 subsequent ticks. Derived broad-phase data may be rebuilt only if canonical processing order remains unchanged. Corrupt or incompatible snapshots fail clearly.
