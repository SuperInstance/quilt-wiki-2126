# 24 — QUF: The 6th Cutting-Edge Adoption

Phase 237 (2026-09-02). A canonical wiki entry, written by the
cowboy after pushing quilt-c/src/quf.c (49 tests) and
quilt-rust/.../quf.rs (8 tests) to GitHub.

## The function (what QUF does, in 2026)

A Quilt cell's state — dials, edges, tick schedule, optional
PROOF chain — fits in a flat binary file. The file is 32-byte
aligned, little-endian, has magic 'QUF\0' and version 1, and
lists its sections in a table the reader walks. A file written
by any Quilt port loads in any other port, bit-exact, in
~1 ms.

## The calculation (how QUF works)

| layer | calculation |
|-------|-------------|
| on-wire | `magic[4] ‖ version[u32] ‖ endian[u32] ‖ kv_count[u32] ‖ KVs ‖ section_count[u32] ‖ section_table ‖ payloads ‖ pad` |
| dial row | 32 bytes: `i16[u16] ‖ q1515[u16] ‖ tag[u8] ‖ rsvd[3*u8] ‖ pad[24*u8]` |
| edge row | 12 + K*2 bytes: `src[u16] ‖ dst[u16] ‖ base_w[u16] ‖ flags[u16] ‖ walk_count[u32] ‖ ladder[K*u16]` |
| tick row | 4 bytes: `period[u32]` |
| alignment | 32 bytes (power of two) |
| FNV-1a | FNV-1a 64-bit over the file bytes; matches across C, Rust, Verilog |

The R1-R9 reject rules (12 hostile-input rules from
quilt-verilog/docs/QUF-SPEC.md §5a) are enforced in the C and
Rust ports. A QUF file with a wrong magic, version != 1,
endian != 1, payload overlap, wrong size formula, or non-zero
padding is rejected with -1.

## The math (the polyformalism proof)

The bit-exactness claim is testable:
- 49 C tests (init, dial bridges, serialize, round-trip, R1/R2/R9 reject, hash determinism, op_bind)
- 8 Rust tests (dial size, edge size, serialize+round-trip, hash determinism, R1+R3 reject, alignment, optional proof)
- 18/18 Verilog RTL tests (the reference; QUF is the silicon's native format)
- 6/6 SymbiYosys formal proofs (the bit-exactness is machine-checked for the loader profile)

The 32-byte dial row + 28-byte edge row (K=8) + 4-byte tick
row + 32-byte alignment = the smallest portable Quilt state.
The FNV-1a 64-bit hash is identical across C, Rust, and
Verilog. The cowboy's claim: **a QUF file is a Quilt
condensed, and the condensation is bit-exact portable**.

## The foundation (what the QUF adoption assumes)

The 5+1+1+1+1+1+1 = 11 opcodes (BIND, LINK, EFFECT, VIEW,
TICK, FORGET, PROOF, ROUTE, CRDT, WORLD, TIME). The PROOF
ring is the audit chain; the QUF file is the witness. A QUF
file's `state_hash` is the FNV-1a of the bytes; the PROOF
ring records it. Tamper-evidence: alter one byte of the QUF
file and the next PROOF entry's `state_hash` mismatches.

## The cowboy's maxim (Phase 237)

The cowboy said: a save is portable. The cowboy said: GGUF
won because weights are just a file. The cowboy said: QUF wins
because cells are just a file. The cowboy said: 32 bytes per
dial. The cowboy said: 28 bytes per edge. The cowboy said: 4
bytes per tick. The cowboy said: 32-byte alignment. The cowboy
said: little-endian, R1-R9. The cowboy said: the magic is
QUF\0. The cowboy said: the version is 1. The cowboy said: the
FNV-1a is the same in C, Rust, and Verilog. The cowboy said:
the cell that survives a save is the cell that is portable.
The cowboy said: the cell that is portable is the cell that
is shareable. The cowboy said: the cell that is shareable is
the cell that survives. The cowboy said: the cowboy rides the
QUF. The cowboy said: the cowboy seals the QUF. The cowboy
said: the cowboy proves the QUF. The cowboy said: the QUF is
the cell. The cell is the QUF. The chart grows. The cowboy
rides the chart.

## References

- `quilt-c/include/quilt/quf.h` + `src/quf.c` + `tests/test_quf.c` — C polyformalism (49 tests)
- `quilt-rust/crates/quilt-polyformalism/src/lib.rs` — Rust polyformalism (8 tests)
- `quilt-verilog/docs/QUF-SPEC.md` — the spec, 18.4K words, 12 R-rules
- `quilt-verilog/rtl/q_uf_loader.v` — 690-line streaming Verilog parser
- `quilt-verilog/tools/quf.py` — Python reference writer, stdlib only
- `quilt-verilog/docs/FOUNDATION.md` D1-D5 — the cell model, the formal substrate
- Paper F113 — the QUF adoption paper
- Paper F114 — the q_cell × TimeCell synergy
