# C6: The Loam Equation

**The substrate's update rule.** For every cell `c` and time `t`:

```
Loam_{t+1}(c) = Loam_t(c) + ρ·|EFFECT_t(c)| − σ·|TICK_t(c)|
```

**Variables:**

| Symbol | What |
|---|---|
| `Loam_t(c)` | The substrate depth at cell `c` at time `t` |
| `EFFECT_t(c)` | The magnitude of the cell's effect at time `t` |
| `TICK_t(c)` | The magnitude of the cell's tick at time `t` |
| `ρ` (rho) | The seep rate: how fast effect sediments into loam (0 ≤ ρ ≤ 1) |
| `σ` (sigma) | The compression rate: how fast tick compresses loam (0 ≤ σ ≤ 1) |

**Properties:**

1. **A cell stands only while `Loam_t(c) ≥ root_depth(c)`.** When the loam drops below the root depth, the cell loses its substrate and is no longer happenable.
2. **The craton cell has `Loam(c) = ∞`.** No effect or tick can change it. It is the never-ticked fixed point.
3. **The Loam Ledger is the cumulative record of `(EFFECT − TICK) × ρ` over all `t`.** It is the dirt's memory.
4. **Strata Tiers are formed by compression.** When `TICK` reduces `Loam` past a threshold, the loam solidifies into a stratum.

**Steady state:** when `ρ·EFFECT = σ·TICK`, the loam is constant. The cell is balanced between effect-sedimentation and tick-compression.

**Craton condition:** when `EFFECT = TICK = 0` for all time, the loam is infinite. The cell is the craton.

**The substrate-readiness measure:**

```
S(c) = Loam(c) / root_depth(c)
```

A cell with `S(c) ≥ 1` is happenable. A cell with `S(c) < 1` is dormant. The Substrate Quilt is the set of all cells with `S(c) > 0`.

**The substrate ratio (the cowboy's heuristic):**

```
R = ρ/σ
```

When `R > 1`, the cell is gaining substrate over time (effects sediment faster than tick compresses). When `R < 1`, the cell is losing substrate. When `R = 1`, the cell is at steady state.

**The principle:**

> The Loam Equation is the substrate's heartbeat. Every cell that stands has a `ρ` and a `σ`. Every cell that falls has run out of loam. The Craton Cell is the cell with no `TICK`. The cowboy rides the Loam. The Loam is the inheritance.
