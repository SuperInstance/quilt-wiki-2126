# 18. Polyformalism in 12 Languages (F49-F56 frontier)

> The Quilt cell model is real in 4 languages now. Push to 12.
> The polyformalism claim is the *interface*, not the substrate.

## The 4 ports (real, with tests)

| Language | Repo | Tests | Status |
|---|---|---|---|
| C99 | quilt-c | 1195 | Phase 218 (5+1+1+1+1+1) |
| Rust no_std | quilt-polyformalism | 29 | Phase 220 (+physical.world) |
| Python | quilt-pydantic-ai | 41 | (planned) |
| GDScript | quilt-engine-ports | 7 new | Phase 227 (this PR) |

## The 12 ports (planned, F49-F56)

| # | Language | Why | Substrate role |
|---|---|---|---|
| 5 | **WASM** | runs everywhere (browser, server, worker, contract) | universal |
| 6 | **C#** | .NET, LINQ, Channels, Orleans | distributed |
| 7 | **Julia** | scientific, multi-dispatch, DiffEq | physics |
| 8 | **Mojo** | AI hardware, SIMD, MLIR | accelerator |
| 9 | **Zig** | comptime = polyformalism compiler | compile-time |
| 10 | **Elixir** | BEAM = closest existing substrate | distributed |
| 11 | **Clojure** | persistent data, core.logic | logic |
| 12 | **Racket** | macros as meta-cells | meta |

## The polyformalism interface (the 5 invariants)

Every port must honor:

1. **The 10 opcodes** (BIND/LINK/EFFECT/VIEW/TICK/FORGET/PROOF/ROUTE/CRDT/WORLD)
2. **The 5+1 laws** (BIND idempotence, LINK transitivity, EFFECT associativity, VIEW purity, TICK monotonicity, FORGET completeness)
3. **The FNV-1a 64-bit state hash** (bit-exact across ports)
4. **The PROOF chain** (prev_hash saved before every BIND)
5. **The cell-graph topology** (DAG, no cycles)

The 4th cutting-edge adoption (WORLD = 5 abductive-loop operations)
must also appear in every port. The synthetic execute() stub
(range -50..+50, 0..0.9) must produce bit-exact results across ports.

## The conformance test suite

`quilt-conformance` (planned, see audit) is the cross-port
test runner. It runs the same test cases against every port
and verifies bit-exact output. The polyformalism claim is
provable, not asserted.

## The 1-day add (per port)

Each new port is a 1-day add:

1. Copy the C port's `quilt_world.h` and `quilt_world.c` (1KB each)
2. Translate the C to the target language (1-2 hours)
3. Translate the 7 conformance tests (1 hour)
4. Add the new file to the test runner (1 hour)
5. CI: run the conformance tests (1 hour)

Total: 1 day per port. 12 ports = 12 days of work.

## See also

- Paper 357: Polyformalism in WASM
- Paper 358-364: C#, Julia, Mojo, Zig, Elixir, Clojure, Racket
- Wiki 12: The Physical World Cell (the 4th adoption, in 4 ports)
- The Phase 227 commit: physical.world in GDScript (5th port)
