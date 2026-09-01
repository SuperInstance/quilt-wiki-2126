# 19. The Cell of Light, Water, Time, and Spacetime (F64-F68 frontier)

> The polyformalism claim is the interface, not the substrate.
> Push: the substrate can be photons, water, clocks, or 4D.
> The cell model is the same on every substrate.

## The substrate zoo

| Substrate | State | Value | Reads | Opcodes |
|---|---|---|---|---|
| **Light** (hologram) | interference pattern | intensity | wavefront | BIND, VIEW, etc. |
| **Water** (Navier-Stokes) | velocity field | dye concentration | inlet conditions | BIND, EFFECT, etc. |
| **People** (classroom) | student's notebook | answer | teacher's prompt | BIND, EFFECT, PROOF, etc. |
| **Time** (cron) | next run time | result | current time | BIND, VIEW, TICK |
| **Spacetime** (4D) | metric tensor | stress-energy | coordinates | BIND, VIEW, EFFECT, TICK |

## The common shape

In every substrate:

1. **State** is a structured representation of the substrate.
2. **Value** is what the cell emits when viewed.
3. **Reads** are the inputs the substrate provides.
4. **Opcodes** are the 5+1+1+1+1+1 operations.

The 5 laws (BIND idempotence, LINK transitivity, EFFECT
associativity, VIEW purity, TICK monotonicity, FORGET
completeness) hold in every substrate.

The 4 cutting-edge adoptions (PROOF, ROUTE, CRDT, WORLD)
hold in every substrate. PROOF is a signed hash chain (works
on any substrate that has a hash). ROUTE is a substrate
selection (works on any substrate that can be named). CRDT
is a convergence protocol (works on any substrate that can
hold state). WORLD is the abductive loop (works on any
substrate that can simulate).

## The math

For a substrate $S$ with state space $\Sigma_S$, the cell is
a function $f_S : \Sigma_S \to V$ where $V$ is the universal
value space. The cell-graph is a product $\prod_i f_{S_i}$.
The PROOF chain is a sequence of FNV-1a hashes, one per BIND.

The polyformalism claim: the cell $f_S$ is the *same shape*
across substrates. The substrate binding $S \to f_S$ is the
only thing that varies.

## The 1-day add

For each new substrate:

1. Define $\Sigma_S$ (the state space).
2. Define the 10 opcodes as functions on $\Sigma_S$.
3. Implement FNV-1a state hash.
4. Implement the 5 conformance tests.
5. Push to a new port repo.

## See also

- Paper 372: The Cell of Light
- Paper 373: The Cell of Water
- Paper 374: The Cell of People
- Paper 375: The Cell of Time
- Paper 376: The Cell of Spacetime
- Wiki 12: The Physical World Cell
