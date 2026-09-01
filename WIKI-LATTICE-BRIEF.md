# QUILT-WIKI-2126 — "TAKE IT FAR FURTHER" BRIEF

You are the WIKI lane for /home/eileen/projects/quilt-wiki-2126 (clone of github.com/SuperInstance/quilt-wiki-2126). Work on branch `wiki-lattice-v2`, commit incrementally (host has rebooted mid-lane before — save early, save often). DeepSeek/DeepInfra REVOKED. No push without bridge sign-off. Read README.md, INDEX.md, and at least 3 entries per layer before writing anything. The wiki's own doctrine: built BACKWARDS from function to calculation; honesty and coverage limitations are first-class; undersell in prose, let linked depth deliver the holy-shit.

## The three moves (in priority order)

### 1. VERIFY THE LATTICE (the index's promise)
INDEX.md claims "read it forwards or backwards. Both paths are the same path." Audit every entry in 00-future/ and 01-calculations/: does each future-function entry trace DOWN through a calculation → mathematics → foundations chain, and does each foundation trace back UP? The 20 original numbered entries (F1–F7, C1–C5, the 5 math, the 5 foundations) presumably chain; the later cutting-edge entries (time cell, cell of light/water, polyformalism, quilt-JEPA world model, stellar/chemical/meta/physical-world/substrate quilts, f14, l0–l14) almost certainly have dangling or missing rungs. Produce `INDEX-V2.md`: a real adjacency map (function → calc → math → foundation, with gaps marked GAP honestly), plus the missing rung entries themselves — a new calculation or math entry written in the wiki's existing voice ONLY where the chain genuinely needs it (no filler; a GAP left open beats a fake rung — tapestry doctrine).

### 2. MAKE IT RUNNABLE (second example minimum, target 4)
examples/ has exactly one sim (wiki_bake.py). Add runnable kernels that ground the heaviest claims, each a single small Python file with an honest "what this shows / what it does NOT show" header:
- examples/monotone_crystal.py — C4 monotone counting: enumerate/sample monotone boolean functions vs the 2^Θ(2ⁿ/√n) count, show the curve.
- examples/spline_phase.py — C5 phase coupling: integrate θ=ωt+φ around a loop, show nonzero holonomy ∮ωdt and what breaks it.
- examples/hearth_loop.py — F2's self-training loop as a toy discrete dynamical system with a lamp term.
Numeric honesty required: print real numbers, no curve-fitting to the prose. If a sim REFUTES a wiki claim, that's a first-class result — fix the entry and note the correction date.

### 3. WIRE 2126 TO 2026 (the fleet link)
Add a `anchors/` layer: for each of the 5 core functions, one short entry pointing at the REAL 2026 seed in the fleet — e.g. Phased Quilt → quilt-verilog's tick/phase work + Paper 211 tier map; Quilt-JEPA World Model → SuperInstance/elephant (vmf.py, field.py); the 5 opcodes/5 laws → quilt-rust's actual runtime. Anchor entries state plainly: "this is the 2026 seed; here is what exists, here is the gap to 2126." No mysticism, links to real repos/files. This makes the wiki the executable index of the iceberg.

## Deliverables
Branch `wiki-lattice-v2`: INDEX-V2.md, any new rung entries (voice-matched), 2–3 example sims, anchors/ layer, all committed incrementally.

## Report back
Lattice audit verdict (how many chains actually close), rungs added vs GAPs left open, sims written + what they showed (esp. any refutations), anchors wired. The deepest thing you found in the lattice.
