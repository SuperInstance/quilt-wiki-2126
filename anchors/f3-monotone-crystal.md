# ANCHOR F3 — The Monotone Crystal ← its 2026 seeds

*This is the 2026 seed; here is what exists, here is the gap to 2126.*

## The 2026 seeds

- **`quilt-verilog/rtl/q_cell_core.v`** — the TICK decay sweep: every TICK, activity leaks and edges decay. Monotone by construction: state only ever runs DOWN under the clock, and the fire test (`act ≥ thresh ∧ refr = 0`) is one-way. Proven by BMC + k-induction. A finished thought that only ages.
- **`q_hebb_rqh.v` / `q_rqh_bank.v`** — power-law forgetting (RQH): old writes fade as a power law, not an exponential. The 2026 answer to "no board stretchers" — nothing is stretched back, only chiseled away.
- **FORGET** — the 6th opcode exists across the fleet runtimes: a cell can be destroyed without losing the whole (journal survives).

## What exists

Monotone decay under TICK, formally verified; forgetting as power law; FORGET_completeness as law.

## The gap to 2126

- **Monotone by leak ≠ monotone by class.** Nothing in 2026 *enforces* that the fabric computes only monotone functions — the crystal's defining restriction. The count ([C4](../01-calculations/04-monotone-counting.md), corrected 2026-08-31: `log₂|M_n| ~ C(n,⌊n/2⌋)`) measures exactly what a leak-monotone fabric still cannot reach.
- Irreversible single-cut computation: the fabric is reprogrammable (host can rewrite weights); the crystal is a *finished thought* — cut once, never recut.

> The 2026 cell forgets monotonically. The 2126 crystal thinks monotonically. Forgetting is the rehearsal; the finished thought is the premiere.
