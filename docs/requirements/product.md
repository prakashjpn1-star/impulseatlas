# Product requirements

Inspect how a two-dimensional world moves, collides and settles. The numerical core owns geometry, contacts, friction, joints and a deliberately bounded continuous-collision path; the browser explains the results without changing them.

## Purpose

Build a two-dimensional rigid-body physics engine from its numerical core outward. It must detect contacts, resolve collision impulses and friction, enforce mechanical joints, handle a bounded continuous-collision case, and reproduce experiments from tick-stamped inputs. A local browser laboratory will show bodies, contacts, forces, constraints, and numerical errors.

The intended users are developers building small simulations and engineers who want to inspect why a mechanical scene behaves as it does. The central challenge is making interacting approximations remain stable: a collision solver may look convincing for two circles yet fail badly when many bodies stack, joints pull against contacts, or a fast object crosses a thin wall.

This is a numerical simulation and computational geometry project. It is independent of all earlier workflow, messaging, replay, synchronization, gateway, reservation, consensus, streaming, and index-rebuild concepts.

## End state and core ownership

Deliver a reusable simulation library, headless runner, scene format, geometry routines, broad phase, contact manifold generation, iterative impulse solver, joint solver, restricted CCD path, deterministic command playback, snapshots, analytic/reference tests, profiling harness, and browser laboratory.

The engine must implement its own collision and constraint algorithms. Wrapping Box2D, Matter.js, a game engine, or a physics service does not meet the goal. Standard math, JSON, HTTP, and collection libraries are acceptable. Reference engines may inform tests if available, but cannot be required to run the project offline.

## Required scope

Required: static, kinematic, and dynamic bodies; circles; convex polygons with three to eight vertices; compound bodies made of fixtures; mass and rotational inertia; gravity; forces and impulses; collision filtering; broad-phase acceleration; persistent contacts; restitution; Coulomb friction; distance and revolute joints; motor limits; sleeping/waking; fixed-step simulation; circle-versus-static CCD; and inspectable diagnostics.

Deferred: 3D, soft bodies, fluids, deformable materials, fracture, general concave polygon collision, arbitrary dynamic-versus-dynamic CCD, GPU computation, parallel solving, networked multiplayer, and real sound. The first release favors a well-tested CPU solver over a long list of unsupported shape types.
