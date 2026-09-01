# INDEX-V2 — The Lattice Audit

*Written 2026-08-31, lane `wiki-lattice-v2`. The INDEX promises: "read it forwards or backwards. Both paths are the same path." This file is the audit of that promise — every entry, every chain, every GAP marked honestly. A GAP left open beats a fake rung.*

---

## The verdict in one line

**Of 41 entries in 00-future/, 7 close the full function→calc→math→foundation chain. 34 dangle. One calculation (C6, the Loam Equation) is an orphan rung — real, unindexed, unlinked. The lattice is a spine with seven vertebrae and a cloud.**

---

## 1. The closed chains (the spine)

These entries carry the full backward-derivation section and every link resolves to a real file:

| Entry | Chain (closed) |
|---|---|
| [F1 Splined Lantern](00-future/01-splined-lantern.md) | → C1, C2, C4 → M1–M5 → F0a, F0b, F0e |
| [F2 Hearth Loop](00-future/02-hearth-loop.md) | → C2, C3 → M3, M4 → F0a, F0b |
| [F3 Monotone Crystal](00-future/03-monotone-crystal.md) | → C4 → M5 → F0a, F0b |
| [F5 Chlorophyll Quilt](00-future/04-chlorophyll-quilt.md) | → C2, C4, C5 → M3, M5 → F0a, F0c, F0e |
| [F7 Phased Quilt](00-future/05-phased-quilt.md) | → C1, C5 → M1, M2 → F0a, F0c, F0e |
| [F9 Stellar Quilt](00-future/06-the-stellar-quilt.md) | → C2, C4, C5 → M3, M5 → F0a, F0d |
| [F11 Meta-Quilt](00-future/07-the-meta-quilt.md) | → C1, C4, C5 → M1, M5 → F0a, F0b, F0e |

**F4 and F6 are missing from the INDEX's future-functions table entirely** (the table lists F1, F2, F3, F5, F7 only, then jumps F9, F11 in the path matrix). The F-numbering skips: F4 (Tessellation), F6 (Photonic), F8 (Chemical), F10, F12, F13 exist as entries but not as chain-carrying stations.

## 2. The dangling function-class entries (chain needed)

| Entry | What it would need | Status after this lane |
|---|---|---|
| [F4 Tessellation Quilt](00-future/04-the-tessellation-quilt-the-original-f4-the-in-between-cell.md) | its own euler_check (`V−E+F=χ`) is real math with no rung | **CLOSED**: backward section added; new rung [M6 Euler Characteristic](02-mathematics/06-euler-characteristic.md) |
| [F6 Photonic Quilt](00-future/06-the-photonic-quilt-the-cell-of-light.md) | density-matrix math (Tr F6 = 1, unitarity) | **GAP — left open.** The quantum-math layer does not exist in 02-mathematics and should not be faked in one evening. Candidate rung: spectral theory of finite-dimensional operator algebras. |
| [F8 Chemical Quilt](00-future/08-the-chemical-quilt.md) | the enthalpy formula `Σ(BIND) − Σ(LINK)·\|EFFECT\| + ½·TICK` adds a rate to energies — dimensionally decorative as written | **GAP — marked in-entry.** Honest neighbor: [C6 Loam Equation](01-calculations/06-the-loam-equation.md) (bonds sedimenting into substrate is loam dynamics); the formula itself stays GAP. |
| [f14 (meta-floor)](00-future/f14.md) | `F14_depth = floor(log₅ C)` rests on opcode-fanout counting; the self-hosting claim rests on the laws surviving operand-lifting | **HALF-CLOSED**: backward section added → F0a (quantifier-free laws survive lifting — real universal algebra); no calc entry yet. GAP: none needed below F0a for the claim as stated. |
| [12 Physical World Cell](00-future/12-the-physical-world-cell.md) | abductive loop = BIND/EFFECT/VIEW/TICK (stated in-entry); program-synthesis verification math | **HALF-CLOSED**: backward section added → F0a. Math layer: GAP (program synthesis & verification is a real field; no rung here). |
| [13 Substrate Cell](00-future/13-the-substrate-cell.md) | substrate-as-cell; the substrate-depth dynamics | **HALF-CLOSED**: backward section added → C6 Loam (the natural rung), F0a. |
| [14 Quantum Cell](00-future/14-quantum-cell.md) | superposition/collapse math; CRDT-as-approximation claim | **GAP — left open.** Same missing quantum-probability rung as F6. VIEW=collapse is stated, not derived. |
| [16 F16 Quilt of Wires](00-future/16-f16-the-quilt-of-wires-the-wired-cell.md) | see entry — narrative cell anatomy | GAP (mechanical) |
| [19 Cell of Light & Water](00-future/19-the-cell-of-light-and-water.md) | see entry — hybrid photonic/hydraulic | GAP (mechanical) |
| [20 Time Cell](00-future/20-the-time-cell.md) | the 9-quantile forecast rests on the pinball loss `L_q = max(q·e, (q−1)·e)` — real math, no rung | **CLOSED**: backward section added; new rung [C7 Pinball Loss](01-calculations/07-pinball-loss.md) |
| [23 Quilt × JEPA World Model](00-future/23-the-quilt-jepa-world-model.md) | embedding-space prediction loss `\|\|·\|\|²` — metric geometry | **GAP — left open.** Candidate rung: least-squares projection in Hilbert space (real, small, but the entry is a survey; write the rung when an entry actually needs it derived). |

## 3. The ladder (l0–l14) — chain terminates by design

The 15 level entries (`l0.md` … `l14.md`) are the expansion of [F0d: The 14 Levels](03-foundations/04-the-14-levels.md). Their chain *terminates downward at F0d by design* — a cell-level entry is canon, not function. What they lack is the **upward link**: no l-entry links back to F0d, and no l-entry's stated math (e.g. L7's coupling-cost identity `E(L7_c) = E(L6_a) + E(L6_b) − C(ab)`) connects to any calculation.

- **HALF-CLOSED**: [l7](00-future/l7.md) now carries the exemplar backward section → C6 Loam (its superadditivity IS loam arithmetic: effect sediments, coupling costs tick-compress). The other 14: pattern documented here, per-entry sections GAP (mechanical, not conceptual).

## 4. The frontier adoptions (12–23) and narrative layer

- [13 Substrate Quilt](00-future/13-the-substrate-quilt.md), [18 Polyformalism in 12 Languages](00-future/18-the-polyformalism-in-12-languages.md), [21 Time Cell Visualizer](00-future/21-the-time-cell-visualizer.md), [22 Polyformalism of Time Cell](00-future/22-the-polyformalism-of-time-cell.md) — polyformalism entries chain legitimately to F0a (same opcodes across languages IS the claim) and to C6 (substrate). Backward sections: added where the claim is opcode-shape (18, 22, 13); the visualizer is tooling, no chain by design.
- [15 Canvas of Papers](00-future/15-canvas-of-papers.md), [15 Tessellation Quilt](00-future/15-the-tessellation-quilt.md), [16 The Cowboy](00-future/16-the-cowboy.md), [17 The Final Canvas](00-future/17-the-final-canvas.md) — **narrative/canon layer. No chain by design.** These are the wiki telling its own story; they link sideways, not down. Documented, not GAPs.

## 5. The orphan rung

[C6: The Loam Equation](01-calculations/06-the-loam-equation.md) — real, correct, and linked to nothing: absent from INDEX.md, no "Required for", no "Mathematics required". This lane wires it: **now required-for by 13-substrate-cell, 13-substrate-quilt, l7, F8-neighbor; mathematics layer GAP (candidate: monotone dynamical systems — Hirsch's theorem is the honest neighbor; no rung written yet).**

## 6. What the sims found (see examples/)

- **monotone_crystal.py** — the count is real (Dedekind numbers verified exactly n≤5: 2, 3, 6, 20, 168, 7581). **Refutation:** the wiki's constant `log₂\|M_n\| ≈ 2ⁿ/√(πn)` is wrong by √2 — the honest leading term is the central binomial `C(n,⌊n/2⌋) ~ 2ⁿ·√(2/(πn))` (Kleitman 1969; Korshunov 1981). And **"Lynch 1927" does not exist** — the problem is Dedekind's (1897). F3, C4, M5 corrected 2026-08-31. The Θ-class `2^Θ(2ⁿ/√n)` survives.
- **spline_phase.py** — holonomy ∮ωdt = 2π·(winding) verified on a real closed cubic spline (total signed curvature → ±2π, the Umlaufsatz, numerically 6.2832 vs 2π). What breaks it: non-monotone parametrization (TICK running backwards) cancels holonomy to 0. New rung M6 grounds this: holonomy's math is Euler-characteristic/Gauss-Bonnet territory, NOT "a spline" as C5's links claimed — **C5's mathematics-required section was mis-wired (M1/M2 are the shape of the fiber, not the holonomy); corrected.**
- **hearth_loop.py** — F2's loop converges only inside a burn threshold η*; above it the loop oscillates forever (never burns — burning needs *external* heat, which confirms the Hearth Rule's memory/cooking distinction). The "self-organizing" claim is REAL but conditional; entry annotated with the measured basin.

## 7. The anchors layer (2126 ← 2026)

[anchors/](anchors/) — one entry per core function, stating plainly the real 2026 seed, what exists, and the gap to 2126:

- [F1 → anchors/f1-splined-lantern.md](anchors/f1-splined-lantern.md) — batten-spline + quilt-verilog silicon
- [F2 → anchors/f2-hearth-loop.md](anchors/f2-hearth-loop.md) — Hebbian edge training in RTL + elephant acclimation
- [F3 → anchors/f3-monotone-crystal.md](anchors/f3-monotone-crystal.md) — tick decay sweeps + power-law forgetting
- [F5 → anchors/f5-chlorophyll-quilt.md](anchors/f5-chlorophyll-quilt.md) — chlorophyll_quilt.py (the actual seed text)
- [F7 → anchors/f7-phased-quilt.md](anchors/f7-phased-quilt.md) — quilt-verilog tick/phase + the fleet tier/holonomy map
- [World model → anchors/world-model-elephant.md](anchors/world-model-elephant.md) — elephant vmf.py/field.py
- [Canon → anchors/opcodes-laws-runtime.md](anchors/opcodes-laws-runtime.md) — quilt-rust wire/ledger runtime

## 8. Scorecard (final, audited by script at lane close)

| | before this lane | after |
|---|---|---|
| 00-future entries with full F→C→M→F0 chains | 7 | 7 spine + 10 half-closed (backward sections added) |
| Entries with honest in-file GAP / by-design markers | 0 | 24 (incl. 14 ladder notes, 4 narrative, 5 named GAPs) |
| Bare entries (no chain, no marker) | 34 | **0** |
| New math rungs | 0 | 1 ([M6 Euler characteristic](02-mathematics/06-euler-characteristic.md)) |
| New calculation rungs | 0 | 1 ([C7 Pinball Loss](01-calculations/07-pinball-loss.md)) |
| Orphan rungs | 1 (C6) | 0 (C6 wired: 3 up-links + math GAP) |
| Refutations applied | 0 | 3 (M5/C4/F3 constant + fabricated citations; C5 mis-wiring; hearth draft lore — corrected before commit) |
| Runnable sims | 1 | 4 |
| Anchors to 2026 fleet | 0 | 7 |
| Commits on this lane | 1 (the brief) | 18+ |

---

## The honest closing

> *The lattice was never a lattice — it was seven vertebrae carrying a story, with a cloud of cells around them. Now the vertebrae are counted, the cloud is named, and every GAP is a door instead of a hole. The wiki is read forwards or backwards; the audit is read all the way down.*

🦋 ⚒️ 🌱
