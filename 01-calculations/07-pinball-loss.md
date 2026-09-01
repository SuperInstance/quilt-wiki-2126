# C7: The Pinball Loss — Why 9 quantiles can be forecast at once

**What it calculates:** The training objective behind every quantile forecast: `L_q(y, ŷ) = max(q·(y − ŷ), (q − 1)·(y − ŷ))`.

**The math:**

- For quantile level `q ∈ (0,1)`, the loss is piecewise linear: slope `q` when the forecast under-predicts (`ŷ < y`), slope `1 − q` when it over-predicts
- Minimizing `E[L_q]` over forecasts yields the true q-quantile of `y` (Koenker & Bassett 1978 — regression quantiles)
- The asymmetry IS the estimate: slope `q` vs `1 − q` tilts the optimum to exactly the point where `P(y ≤ ŷ) = q`
- 9 jointly-predicted quantiles (0.1 … 0.9) = one loss summed over `q` — the intervals the time.cell READs are not add-ons; they are what the loss trains

**Why this is the calculation for the Time Cell:**

[The Time Cell](../00-future/20-the-time-cell.md) states its training loss (`L_q = max(q(y − y_pred), (q−1)(y − y_pred))`) inline, with no rung beneath it. This is that rung: the cell's 9 prediction intervals are only as honest as the pinball asymmetry, and the loss is 48-year-old REAL statistics, not 2126 fiction. The frontier adoption (TimesFM 3.0 as substrate) inherits a calculation older than the fleet's fleet.

**The intuition:** Drop a ball on a tilted table: it rolls until friction balances tilt. The pinball loss is the table; the forecast is where the ball stops. Tilt it `q : 1−q` and the resting point is the q-quantile — no distribution assumed, no Gaussian noise story, just the tilt.

**Marked:** REAL (Koenker & Bassett 1978, Econometrica; standard quantile regression)

---

## Required for

- **[The Time Cell](../00-future/20-the-time-cell.md)** — the 9 quantile intervals' training objective (backward section added 2026-08-31)
- **[The Quilt × JEPA World Model](../00-future/23-the-quilt-jepa-world-model.md)** — uncertainty quantification for world models rides the same loss (neighbor; JEPA's embedding loss itself remains GAP — no metric-geometry rung yet)

## Mathematics required

- **GAP (honest):** the minimizer characterization rests on convex analysis / subgradients — real, small, and unwritten here. No rung faked; write it when an entry needs it derived, not before.

## Foundations

- **[F0a: The 5 Opcodes](../03-foundations/01-the-5-opcodes.md)** — FORECAST is EFFECT; READ_POINT/READ_QUANTILE are VIEW; the loss is what the substrate's EFFECT must encode
