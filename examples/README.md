# Worked examples

These small fictional inputs and hand-calculated oracles illustrate the contracts. They are not completed benchmark or acceptance results. All counts, identities and expectations depend on the described isolated setup.

| Example | Schema | Interpretation |
| --- | --- | --- |
| [free-fall-scene.json](free-fall-scene.json) | [scene](../schemas/scene.schema.json) | Run 60 ticks without contacts. Rendering and wall time do not alter the recurrence. |
| [free-fall-oracle.json](free-fall-oracle.json) | [analytic-motion](../schemas/analytic-motion.schema.json) | Semi-implicit y_n=y_0+n*dt*v_0+g*dt^2*n(n+1)/2. This is a hand calculation, not an executed test. |
| [elastic-circles.json](elastic-circles.json) | [scene](../schemas/scene.schema.json) | Identical masses initially touch and approach at 2 m/s. Analytic post-collision velocities swap; momentum/energy tolerances follow requirements. |
| [apply-impulse.json](apply-impulse.json) | [tick-command](../schemas/tick-command.schema.json) | Generation is illustrative; use the actual live handle. A past tick or recycled handle is rejected. |
| [step-request.json](step-request.json) | [step-request](../schemas/step-request.schema.json) | The API checks current run/tick and returns explicit failure instead of silently skipping ticks. |
| [box-shape.json](box-shape.json) | [shape](../schemas/shape.schema.json) | CCW convex rectangle. Semantic geometry validation checks area, winding and intersections beyond JSON shape. |

The free-fall values use the discrete integrator formula, not continuous motion as an incorrectly exact oracle.

Real fixture generators, actual checksum manifests, mandatory large campaigns and raw results remain implementation deliverables. Counterexamples and failed runs must be retained rather than replaced with successful-looking templates.

Additional supported-scope fixture: [ccd-thin-wall.json](ccd-thin-wall.json), validated structurally by the [scene schema](../schemas/scene.schema.json), uses a 150 m/s bullet circle and 0.05 m static axis-aligned wall. The first ideal TOI is (2 - 0.025 - 0.05)/150 seconds before skin/slop policy. It must not be silently treated as ordinary discrete polygon CCD. This is a planned fixture, not an executed tunneling result.
