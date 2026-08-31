# 12. The Physical World Cell (Code-as-World adoption)

> The cell *is* a program. The program simulates a physical
> scene. The scene's quantity is the cell's value. The VLM
> proposes the program from observation. The interpreter
> executes it. The renderer draws it. The verifier checks
> it. The refiner tightens it. The abductive loop runs.

## What is a physical.world cell?

A Quilt cell whose kind is `physical.world`. The cell's state
is a Python program (the "code-as-world"). The cell's value
is a `Quantity { value, uncertainty, unit, verified }`. The
cell's reads are the program's inputs.

The 5 abductive-loop operations:

| # | Op | What it does |
|---|---|---|
| 0 | PROPOSE | Set the program text. BIND. |
| 1 | EXECUTE | Run the program, get a Quantity. |
| 2 | RENDER  | Draw the simulation to an image. |
| 3 | VERIFY  | Compare Quantity to observation. |
| 4 | REFINE  | Append a `# refine: <hint>` and re-PROPOSE. |

## Why this is a cell, not a feature

A feature is a *thing the system does*. A cell is a *thing
the system can be*. The difference: a cell composes. A
physical.world cell can be the input of another cell
(dependency), the output of another cell (dependent), part of
a CRDT (convergent), part of a PROOF chain (auditable),
part of a ROUTE (substrate-routable), part of a tick (re-evaluated).

The 5+1+1+1+1+1 opcodes apply unchanged. The cell model
does not change. The polyformalism is the *kind*.

## The polyformalism: C and Rust

In C:

```c
quilt_world_program_t p;
quilt_world_program_init(&p);
quilt_world_propose(&p, "x = 5; y = x * 2");
quilt_quantity_t q;
quilt_world_execute(&p, NULL, 0, &q);
// q.value is in -50..+50 (synthetic), q.uncertainty in 0..0.9
```

In Rust (no_std):

```rust
let mut cell = WorldCell::new();
cell.propose("x = 5; y = x * 2");
let q = cell.execute_counted(&[]);
// q.value in -50..+50, q.uncertainty in 0..0.9
```

The shape is identical. The synthetic values are identical
(same FNV-1a, same ranges). A real substrate binding (Python
exec() in a sandbox, or Code-as-World-VL-9B for synthesis)
replaces the stub.

## The PROOF chain

Every PROPOSE (BIND) records the previous `state_hash` in
`prev_hash` before overwriting. This is the same pattern as
the Phase 216 PROOF opcode: a hash-linked audit chain. A
tampered program text is detectable: the live `state_hash`
won't match the one in the chain.

In the Code-as-World paradigm, this is the *verification
chain*: every iteration of the abductive loop appends a
link. The paper's "verified" flag is a single bit; the
Quilt cell has the full 32-byte chain.

## The 6th frontier adoption

Phase 216-218: PROOF, ROUTE, CRDT (3 adoptions, all shipped).
Phase 222: WORLD (the 4th adoption, just shipped). The
Quilt opcodes are now 5+1+1+1+1+1 = 10.

The Code-as-World paper proposes: physical scenes are
executable programs. Quilt adopts: a cell *is* a program.
The cell model is general enough to host the proposal.

## The open frontier: substrate binding

The 9B model is on Hugging Face. To use it, we need a
binding to a GPU. Options:

- CF Worker proxy to a HF Inference Endpoint.
- Local distilled 4B variant on the substrate (esp32 won't
  fit; jetson or cf worker fits).
- Stub (the current polyformalism default) for testing.

The polyformalism claim is independent of which substrate
binds. The cell shape is the same in all 3.

## See also

- Paper 320 (this work)
- Paper 308 (L7 + 3 cutting-edge adoptions)
- Paper 319 (polyformalism in 2 languages)
- Paper 315 (L0-L14 foreman-completeness)
- The Code-as-World paper: arXiv 2608.27549
- The Code-as-World-VL-9B model: huggingface.co/MirroS-Lab/Code-as-World-VL-9B
