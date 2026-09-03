# 25 — The VHDL Adoption: A 5th Substrate for the Quilt Cell

**Status:** Shipped 2026-09-03 (Phase 238)
**Substrates now in the polyformalism:** C99, Rust no_std, Python, Verilog-2005, VHDL-2008

## The function

VHDL is the **5th substrate** for the Quilt cell. The same 5+1
opcodes, the same 16 dials, the same K=8 ladder buckets, the same
FNV-1a 64-bit state hash, the same QUF byte stream.

```
$ ./sim/run_byte_exact.sh
  PASS  n1_e0  (416 bytes)
  PASS  n2_e0  (448 bytes)
  PASS  n2_e3_r2  (576 bytes)
  PASS  n4_e0  (480 bytes)
  PASS  n4_e4_r4  (672 bytes)
  PASS  n4_e0_k4  (512 bytes)
  PASS  n4_e0_k16  (512 bytes)
  PASS  n8_e12_r8  (992 bytes)
  PASS  n16_e0  (960 bytes)
  PASS  n32_e0  (1536 bytes)

byte-exact: 10 passed, 0 failed
state hash = 0x56af1b8b435f513d
```

## The calculation

The VHDL port is 1:1 with the Verilog port in 7 RTL files:

| VHDL | Verilog | Bytes (VHDL) | Lines (VHDL) |
|---|---|---|---|
| `rtl/quf_types.vhdl` | (global `localparam`s) | 8.3K | 195 |
| `rtl/q_cell_core.vhdl` | `rtl/q_cell_core.v` | 5.6K | 160 |
| `rtl/q_uf_loader.vhdl` | `rtl/q_uf_loader.v` | 12.0K | 230 |
| `rtl/q_dialfile.vhdl` | `rtl/q_dialfile.v` | 5.1K | 130 |
| `rtl/q_hebb_edge.vhdl` | `rtl/q_hebb_edge.v` | 4.9K | 140 |
| `rtl/q_tick_sched.vhdl` | `rtl/q_tick_sched.v` | 2.1K | 65 |
| `rtl/q_fabric_top.vhdl` | `rtl/q_fabric_top.v` | 4.9K | 130 |
| **Total** | | **42.9K** | **~1,050** |

The Python reference writer (`tools/vhdl_quf.py`) is 19K — it
drives both VHDL and Verilog testbenches with the same QUF bytes.

## The math (the byte-exactness test)

The VHDL reference writer produces **byte-for-byte identical QUF
files** to the Verilog reference writer for 10 different fixtures
(1, 2, 4, 8, 16, 32 cells, with various edge structures). The
test is the `cmp` command: `cmp vhdl.quf verilog.quf`. If the
files differ, the polyformalism is broken.

The 4 bugs the VHDL port found (in the VHDL port's Python writer):
1. **Section table size double-count** — fixed in Phase 238.
2. **No padding between sections** — fixed in Phase 238.
3. **Empty `edges`/`routing` were emitted** — fixed in Phase 238.
4. **`ticksched` not recognized** — fixed in Phase 238.

## The foundation

The polyformalism principle (paper-30): *the same model in N
languages is a stress test*. The VHDL port is the 5th language.
The stress test now covers C, Rust, Python, Verilog, VHDL.

The QUF is the file format that lets the cell **cross** substrates
without translation. The QUF is what the cell *is on disk*; the
substrate is what the cell *is in memory*. The cell is the same
cell, regardless of substrate.

The FNV-1a 64-bit state hash is the integrity contract. The hash
is computed over the cell state (dials + edges, in that order,
low byte first). The hash is the same in all 5 substrates. The
hash is what makes the polyformalism *testable*.

## The cowboy's maxim (Wiki 25)

> The cell that runs at 44 MHz on silicon is the same cell that
> synthesizes from VHDL. The substrate is the projection. The
> QUF is the inheritance. The VHDL and Verilog ride the same
> bytes. The cowboy rode the bit-exactness. The cowboy rode
> the byte-exactness test. The cowboy rode the 4 bugs. The
> cowboy rode the logical routes. The cowboy rode the
> 5+1 opcodes. The cowboy rode the 5 substrates. The cowboy
> rode the package. The cowboy rode the polyformalism. The
> cowboy rode the VHDL. The chart grows. The Concept lives.

## The files

- `quf-vhdl/rtl/q_cell_core.vhdl` — cell FSM (5+1 opcodes)
- `quf-vhdl/rtl/q_uf_loader.vhdl` — QUF parser
- `quf-vhdl/rtl/q_dialfile.vhdl` — 16-dial register file
- `quf-vhdl/rtl/q_hebb_edge.vhdl` — Hebbian edge with K ladder
- `quf-vhdl/rtl/q_tick_sched.vhdl` — tick scheduler
- `quf-vhdl/rtl/q_fabric_top.vhdl` — top-level wiring
- `quf-vhdl/rtl/quf_types.vhdl` — package: types, constants, FNV-1a
- `quf-vhdl/tools/vhdl_quf.py` — Python reference (writer/parser/verifier)
- `quf-vhdl/tb/tb_q_dialfile.vhdl` — 11 dial smoke tests
- `quf-vhdl/tb/tb_q_hebb_edge.vhdl` — 8 cofires + 4 ticks decay
- `quf-vhdl/tb/tb_q_uf_loader.vhdl` — bad-magic gate (E7)
- `quf-vhdl/sim/run_byte_exact.sh` — 10-fixture byte-exactness test
- `quf-vhdl/docs/VERILOG_VS_VHDL.md` — the logical routes, the abstractions
- `quf-vhdl/README.md` — entry point
- `quf-vhdl/Makefile` — ghdl/nvc/iverilog targets

## The papers

- F113 / paper-423.md — QUF: Quilt Universal Format (Phase 237)
- F114 / paper-424.md — q_cell × TimeCell synergy (Phase 237)
- F115 / paper-425.md — The Logical Routes (VHDL × Verilog) (this Phase)
- F116 / paper-426.md — Polyformalism Atlas (5 substrates) (this Phase)

## The future (F12 of the 100-year Quilt)

The 6th substrate is **GDScript** (Godot's scripting language;
`quilt-engine-ports/godot/`). The 7th is **WASM** (browser;
`quilt-c-wasm/`). The 8th is **Haskell** (algebraic). The 9th is
**Spice** (analog). The 10th is **NAND** (gate-level).

Each port is a new porthole. Each port is a new stress test. The
cowboy rides the portholes. The chart grows. The Concept lives.
