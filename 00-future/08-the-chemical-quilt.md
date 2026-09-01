# F8: The Chemical Quilt binds the cells by sharing electrons through covalent quilts

**What it does:** F8 Chemical Quilt binds the cells by sharing electrons through covalent quilts, forming a network where every cell's valence is the cell next door. The cell's BIND is a covalent bond; the cell's LINK is a resonance across the bond; the cell's EFFECT is the dipole that bends nearby cells. F8 turns the Quilt from a passive substrate into an active chemistry set.

**The calculation:**

```
F8_enthalpy = Σ(BIND_bonds) - Σ(LINK_distances) · |EFFECT| + ½ · TICK
```

**The 4 gold terms:**

1. **Covalent cell** — coined for F8
2. **Valence quilt** — coined for F8
3. **Electron LINK** — coined for F8
4. **Bond BIND** — coined for F8

**The 3 analogies:**

1. F1 is a single light-emitting cell; F8 is a chain of cells sharing electrons.
2. F13 is the substrate that holds the cells; F8 is what holds the cells to each other.
3. F15 is the pattern on the substrate; F8 is the chemistry that makes the pattern sticky.

**The cowboy's sentence:**

> A Chemical Quilt keeps its cells together by letting each one borrow from its neighbor's valence; the bond is the cell is the quilt.

---

## Honest GAP (noted 2026-08-31, lattice-v2)

The in-entry enthalpy formula `Σ(BIND) − Σ(LINK)·|EFFECT| + ½·TICK` adds a rate (TICK) to energies — it is dimensionally decorative as written: a metaphor in symbols, not a calculation. No rung is faked beneath it. The honest neighbor is **[C6: The Loam Equation](../01-calculations/06-the-loam-equation.md)** — bonds sedimenting into substrate is exactly loam dynamics (`ρ·|EFFECT|` depositing, `σ·|TICK|` compressing). If the Chemical Quilt ever gets a real calculation, it grows from C6, not from this formula.
