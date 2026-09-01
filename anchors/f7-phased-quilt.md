# ANCHOR F7 — The Phased Quilt ← its 2026 seeds

*This is the 2026 seed; here is what exists, here is the gap to 2126.*

## The 2026 seeds

- **`quilt-verilog`** — the fabric-wide **tick**: every cell advances under one clock; `OP_TICK = 4` runs the decay sweep, the fire test, the fanout. Phase discipline exists as the QUF flat state file: the entire fabric's state — every dial, every weight, every phase counter — travels in one binary that a testbench, a soft core, or an FPGA loads identically. θ = ωt + φ has a 2026 shadow: the per-cell tick counters carried in QUF.
- **`quilt-cellular-arch/fleet/FLEET_HANDOFF.md`** — the tier/holonomy map: "the same 5 tiers from the Framed Quilt apply to the fleet" — totipotent (full holonomy) through synovial (variable), each boat placed by how much rotation it still carries; myelinated boats move DOWN the tiers, wounded boats UP. This is the document the wiki's tier map (F0c) points at. *(Note, honestly: the wiki's "Paper 211" numbering is 2126-side; no literal Paper 211 exists in the 2026 fleet — the tier map's real home is this file.)*

## What exists

One fabric-wide clock in silicon, formally proven (the tick's ingress-drop hole was found and fixed by the proofs); a fleet tiered by holonomy with doctrine for motion between tiers.

## The gap to 2126

- The fiber bundle is a metaphor, not a structure: no per-cell SO(3) frames, no connection 1-forms, no geometric holonomy. The journal's prev-hash chain is *bookkeeping* holonomy — [examples/spline_phase.py](../examples/spline_phase.py) shows what the geometric version would have to measure (2π·winding, and mixed-sign ticks cancelling it to zero).
- θ linking temporal and spatial origins: the 2026 tick is global wall-clock order; the 2126 phase is per-cell origin linking. The distance between them is the whole fiber-bundle layer ([C5](../01-calculations/05-spline-phase-coupling.md) → [M6](../02-mathematics/06-euler-characteristic.md)).

> The 2026 fabric keeps time. The 2126 quilt keeps phase. One clock tells you when; a fiber bundle tells you how far you turned getting there.
