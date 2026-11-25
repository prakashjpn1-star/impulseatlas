# JSON Schema catalog

These draft-2020-12 schemas describe proposed version 1 request/data shapes. They complement the [domain contracts](../docs/contracts/data-and-artifacts.md) and [artifact specifications](../formats/README.md), not a running product.

| Schema | Purpose |
| --- | --- |
| [shape.schema.json](shape.schema.json) | Supported circle or convex polygon shape |
| [joint.schema.json](joint.schema.json) | Distance or revolute joint |
| [tick-command.schema.json](tick-command.schema.json) | Ordered tick-boundary command |
| [scene.schema.json](scene.schema.json) | Version 1 deterministic world scene |
| [step-request.schema.json](step-request.schema.json) | Bounded world advance |
| [snapshot-manifest.schema.json](snapshot-manifest.schema.json) | Complete same-build snapshot identity |
| [analytic-motion.schema.json](analytic-motion.schema.json) | Hand-calculated motion oracle |

Semantic core checks go beyond JSON structure: finite parser values, decoded byte limits, exact identities, geometry/convexity, graph connectivity, cost overflow, type/effect legality or run state are checked by the relevant importer/service. Proposed array/string/work maxima are explicit design defaults pending target-environment verification. No real tokens or fabricated fixture hashes appear in examples.

These projects use versioned artifacts and owned memory. A database schema is not forced onto numerical arrays, graph preprocessing or a VM heap. The [format notes](../formats/README.md) specify those structures instead.

Velocity shape permits the 150 m/s bullet case; runtime vector magnitude and ordinary-versus-bullet limits remain semantic checks. Force/impulse components use a separate proposed ±1e9 bound, not the ±100 m world-coordinate domain. No input is silently clamped.
