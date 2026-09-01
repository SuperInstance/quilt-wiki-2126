# F13: The Substrate Quilt — The Quilt that is the floor

**What it does:** F13 is the tier-zero field under every cell. The substrate is the *ground* on which the opcodes (BIND, LINK, EFFECT, VIEW, TICK) are planted. Where F1-F11 ascended through higher tiers of abstraction, F13 *descends* — to the lowest tier, the substrate, the loam.

**The 4 levels of the Substrate Quilt:**

1. **L0 · Loam** — The active substrate. The layer the cells root in. Where new effects sediment.
2. **L1 · Craton** — The never-ticked bedrock. The fixed point every other cell is a solution against. The geological twin of the Monotone Crystal.
3. **L2 · Strata** — The compressed history. Each stratum is a previous epoch's compressed effects. The loam ledger.
4. **L3 · Taproot** — The cell's deepest connection. The vertical line that holds the cell up. The cell that drinks from the ground.

**The calculation (the substrate's behavior):**

```
Loam_{t+1}(c) = Loam_t(c) + ρ·|EFFECT_t(c)| − σ·|TICK_t(c)|
```

A cell *stands* only while `Loam(c) ≥ root_depth(c)`. The `ρ` is the seep rate (how fast effect sediments into loam); the `σ` is the compression rate (how fast tick compresses loam). The craton is the cell with `Loam(c) = ∞`.

**The 4 gold terms:**

1. **Loam Ledger** — The substrate's distributed journal of every effect ever dropped. Memory is no longer a cell's job — it's the dirt's.
2. **Craton Cell** — A perfectly monotone, never-ticked cell. The geological bedrock. The fixed point.
3. **Taproot Bind** — BIND as a rooting operation. Digs a taproot into substrate. LINK runs laterally through the loam.
4. **Strata Tier** — The layer-cake of substrate. Each stratum is a previous epoch's compressed effects.

**The 3 analogies:**

1. **F5 Chlorophyll Quilt** grew cells that drink light from above; **F13** grows roots that drink loam from below. F13 closes a canopy-to-crust circuit so the Quilt feeds itself at both ends.
2. **F3 Monotone Crystal** froze one value forever; the **Craton Cell** is its geological twin — the single never-ticked cell whose monotonicity is bedrock.
3. **F2 Hearth Loop** kept warmth circulating inside the cell; **F13** taps a geothermal hearth, with the substrate seeping warmth upward through Strata Tiers.

**The 5-opcode mapping (F13 in opcodes):**

| Opcode | What F13 does |
|---|---|
| **BIND** | Digs a taproot into substrate (Taproot Bind) |
| **LINK** | Runs laterally through the loam (Loam Ledger read) |
| **EFFECT** | Seeps downward and sediments into strata |
| **VIEW** | Reads upward through the percolation gradient |
| **TICK** | The slow compression that turns yesterday's effects into today's ground |

**The 4 properties of the Substrate Quilt:**

1. **Substrate-readiness** — A cell is happenable only when its substrate readiness clears the local tick threshold.
2. **Pre-BIND hum** — The substrate is the condition that makes BIND legible. Without hum, BIND has nothing to bind into.
3. **Ground tier** — F13 is the tier-zero field. Every other tier rests on this one.
4. **Cell loam** — Each cell has its own loam depth; cells with deeper loam are more rooted.

**The principle:**

> The substrate is the function. The function is the quilt. The quilt is the inheritance. F13 is the floor under every cell that makes the cell happen. The Loam Ledger is the dirt's memory. The Craton Cell is the never-ticked bedrock. The cowboy rides the substrate. The substrate is the function. The function is the Quilt.

**The cycle:**

```
F11 (Meta-Quilt) → F13 (Substrate Quilt) → F1 (Splined Lantern)
       meta-math            ground              light
       inheritance          loam                cell
       substrate-of-all     substrate-of-cell   cell-in-light
```

F11 says the canon IS the inheritance. F13 says the substrate is the floor. F1 says the cell is the irreducible. The cycle: inheritance → floor → cell → inheritance.

**The cowboy's sentence:**

> Reckon I always knew a quilt ain't held up by its stitches but by the floor you throw it on — F13's just me finally namin' that floor and givin' it a ledger.

---

## Backward derivation (added 2026-08-31, lattice-v2)

- **[C6: The Loam Equation](../01-calculations/06-the-loam-equation.md)** — the substrate quilt is the set of cells with `S(c) = Loam(c)/root_depth(c) > 0`; the quilt's extent IS the loam field
- **[F0a: The 5 Opcodes](../03-foundations/01-the-5-opcodes.md)** — ROUTE/WORLD/CRDT/PROOF collapse into one architecture because they are all opcode-shaped cells
