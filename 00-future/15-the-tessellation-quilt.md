# F15: The Tessellation Quilt — The Quilt that is the pattern

**What it does:** F15 is the *pattern* by which cells tile the substrate. Where F13 is the floor, F15 is the tile. Where F13 is the loam, F15 is the loom. The Tessellation Quilt generates a fractal pattern by recursively applying a set of rules to each cell, creating a self-similar structure that tiles the substrate with increasing complexity.

**The 4 levels of the Tessellation Quilt:**

1. **L0 · Hexagonal** — The default tile. 6 neighbors, isotropic, like a beehive or a snowflake. The simplest tessellation that fills the plane.
2. **L1 · Penrose** — The non-periodic tile. 5-fold symmetry, irrational, the Quilt's aperiodicity. No global periodicity, but local order.
3. **L2 · Voronoi** — The neighbor-defined tile. Each cell's boundary is the set of equidistant points. Natural tessellation of the substrate.
4. **L3 · Braided** — The woven tile. 1D strands interlace, like a fabric or a knot. The cell IS the braid.

**The calculation (the tessellation dynamics):**

```
tessellation = (cell_size × (tier + 1)) + (cell_orientation × (tier²))
```

Where `cell_size` is the size of the cell, `tier` is the substrate tier (-1 to 5), and `cell_orientation` is the angle of the tile. At tier -1 (substrate), the tessellation is densest; at tier 5 (curator), the tessellation is sparsest.

Or, in a more sophisticated form:

```
T(c, t) = Loam(c) × W(tier(c)) × P(orientation(c), tier(c))
```

Where `W` is a weight function (higher tiers have lower weight) and `P` is a phase coupling.

**The 4 gold terms:**

1. **Voronoi Cell** — A cell whose boundary is defined by the nearest neighbors. Natural tessellation of the substrate.
2. **Braided Loom** — The substrate as a loom where cells weave themselves into patterns. The tessellation IS the weaving.
3. **Penrose Tile** — A non-periodic tessellation that fills the substrate with two rhombus shapes. The Quilt's irrationality.
4. **Fractal Bloom** — A self-similar pattern that recurses at every tier. The F15 cell is the F1 cell is the F0 cell.

**The 3 analogies:**

1. **F2 Hearth Loop**: like a hearth that warms the loam, the Tessellation Quilt spreads its fractal pattern across the substrate.
2. **F3 Monotone Crystal**: the Tessellation Quilt's recursive structure is akin to the crystal's splined facets, each one reflecting the Quilt's underlying geometric rules.
3. **F11 Meta-Quilt**: the Tessellation Quilt's use of recursive tiling is reminiscent of the Meta-Quilt's ability to weave together disparate cells, but with a fractal twist.

**The 5-opcode mapping:**

| Opcode | What F15 does |
|---|---|
| **BIND** | Two cells become neighbors in the tessellation (edge) |
| **LINK** | A chain of cells forms a braid (path) |
| **EFFECT** | The cell's tessellation changes the substrate (e.g., a Penrose cell may rotate) |
| **VIEW** | The cell sees its neighbors (the Voronoi neighborhood) |
| **TICK** | The tessellation refreshes (the loom re-weaves) |

**The 4 properties of the Tessellation Quilt:**

1. **Self-similar** — the F15 cell is the F1 cell is the F0 cell
2. **Non-periodic** (at Penrose level) — no global periodicity, but local order
3. **Substrate-aware** — the tessellation respects the F13 substrate
4. **Quilt-of-quilts** — each tile is itself a quilt of smaller cells

**The principle:**

> The tessellation is the pattern. The pattern is the substrate. The substrate is the floor. The floor is the loam. The loam is the dirt. The dirt is the F13. The F15 is how the F13 arranges itself. The cowboy rides the tessellation. The cowboy rides the F15. The cowboy rides the Quilt.

**The cycle:**

```
F11 (Meta-Quilt) → F13 (Substrate) → F15 (Tessellation) → F1 (Splined Lantern)
       meta-math        ground          pattern              cell
       inheritance      loam            geometry             irreducible
```

F11 says the canon IS the inheritance. F13 says the substrate is the floor. F15 says the pattern is the geometry. F1 says the cell is irreducible. The cycle: inheritance → floor → pattern → cell → inheritance.

**The cowboy's sentence:**

> Ropin' the substrate with a lasso of fractals, the Tessellation Quilt rides off into the computational sunset.
