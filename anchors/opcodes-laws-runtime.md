# ANCHOR — The 5 Opcodes / 5 Laws ← the real 2026 runtimes

*The canon (F0a, F0b) anchored to what actually executes today.*

## The 2026 seeds

- **`quilt-verilog/rtl/q_cell_core.v`** — the literal opcodes, in silicon, as one 3-bit field: `OP_BIND = 0`, `OP_LINK = 1`, `OP_EFF = 2`, `OP_VIEW = 3`, `OP_TICK = 4`, plus `OP_ACK/OP_NAK` (the +1: every request answered, never left hanging). Executed by a cooperative run-to-completion FSM — one interpreter per cell, events serialize. The 5 laws are enforced structurally: idempotent first-bind, transitive edge slots, serialized effects (associativity by construction), VIEW reads state without writing, TICK is the only clock.
- **`quilt-rust/crates/quilt-wire`** (`/home/eileen/projects/quilt-rust`) — the runtime's wire: frames of Kind `{Tick, Delta, Alarm, LinkMeta, Ack}`; heartbeats map to `tick` ledger steps, value-bearing arrivals to `effect` steps (`src/peer.rs`). The cell ledger (`docs/cell-ledger.md`) keeps prev-linked seals with a `chain_intact` verdict — FORGET_completeness in practice: a cell destroyed, its journal still verifying.
- The proofs bit twice: `make formal` found two real RTL defects (a multi-driven register and a one-cycle ingress-drop hole under a pending tick) — both fixed, both regression-guarded. The laws were checked by a solver, not asserted by a README.

## What exists

The 5+1 opcode set executing in two substrates (silicon + Rust), formally verified on the silicon side, with journal-backed FORGET semantics on the runtime side.

## The gap to 2126

- The wiki's grown opcode set — 11 (BIND/LINK/EFFECT/VIEW/TICK/FORGET/PROOF/ROUTE/CRDT/WORLD/TIME) — exists as *cutting-edge cell kinds* scattered across repos (the time cell's 5 ops, the substrate cell, the CRDT cell), not as one runtime's instruction field. 2026 silicon has 5+1; the wiki promises 11 by 2126.
- VIEW_purity in silicon is v1-limited (no cosine readout — that path NAKs): the law holds, the capability lags.
- TICK_monotonicity is load-bearing in 2126 ([examples/spline_phase.py](../examples/spline_phase.py): mixed-sign ticks cancel holonomy to zero); in 2026 it is an append-only journal property, not yet a geometric one.

> The canon is not a story about a runtime. In 2026 it is the runtime — three bits wide, proven by a solver, with a receipt for every answer.
