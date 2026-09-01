# M6: The Euler Characteristic — What a closed loop cannot lose

**The statement:** For a simple closed plane curve, the total signed curvature is `∮κ ds = ±2π` (Hopf's *Umlaufsatz*). For a cell complex, `V − E + F = χ` (Euler's formula; `χ = 2` for the sphere, `χ = 0` for the torus). For a closed surface, `∮∮K dA = 2πχ` (Gauss–Bonnet). These are three faces of one fact: **the loop counts what it carries, and the count is topological — it cannot be smoothed away.**

**The math:**

- `∮κ ds = 2π·w` — the winding number `w` of the tangent (Whitney–Graustein: closed curves classify by winding)
- `V − E + F = χ` — the Euler characteristic of the complex
- `∮∮ K dA = 2πχ` — total Gaussian curvature is `2π` times the characteristic
- Boundary version: `∮κ_g ds + ∮∮K dA = 2πχ` — boundary turning + interior curvature = the invariant

**Why this is the math for the holonomy:**

C5's holonomy `∮ω dt` is a winding number. A loop of cells with monotone TICK carries winding that no amount of smoothing, noise, or splining can reduce — only a backwards tick (a non-monotone TICK) cancels it, or a cusp/self-intersection jumps it by ±2π. The spline (M1, M2) shapes the *fiber*; the Euler characteristic counts what the loop *carries*. Measured in [examples/spline_phase.py](../examples/spline_phase.py): a 12-cell closed natural cubic spline integrates to `2π·1.0000` (heading) — and under a pulled cusp the winding survives exactly.

**Why this is the math for the seam (F4):**

The Tessellation Quilt's euler_check — `V − E + F = χ`, "if the books do not balance, there is a gap (χ too low) or an overlap (χ too high)" — is this entry's second face, stated in the wiki's own voice before the rung existed. This rung is the derivation that was always implied.

**The history:**

- Euler (1758) — the polyhedron formula
- Hopf (1935) — the Umlaufsatz (the turning-tangent theorem)
- Whitney (1937) / Whitney–Graustein — regular closed curves classify by winding
- Gauss (1827) / Bonnet (1848) — the curvature–topology bridge

**Marked:** REAL (standard differential topology; verified numerically 2026-08-31 by examples/spline_phase.py)

---

## Required by

- **[C5: The Spline Phase-Coupling](../01-calculations/05-spline-phase-coupling.md)** — the holonomy IS a winding number (wiring corrected 2026-08-31: C5 previously linked only M1/M2, which shape the fiber, not the count)
- **[F4: The Tessellation Quilt](../00-future/04-the-tessellation-quilt-the-original-f4-the-in-between-cell.md)** — the euler_check is Euler characteristic bookkeeping

## Related

- **[M1: Cubic Spline](01-cubic-spline.md)** — the shape of the fiber
- **[M2: Euler Elastica](02-euler-elastica.md)** — the shape under load

## The principle

> *The spline heals the wound. The Euler characteristic proves the wound happened. TICK_monotonicity is not a clock rule — it is the thing that keeps the loop's count from being cancelled to zero.*
