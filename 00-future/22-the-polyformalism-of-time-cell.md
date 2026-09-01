# 22. The Polyformalism of the Time Cell

> **Same cell shape across 3 languages. Bit-exact. Provable.**

The Quilt `time.cell` cell kind is implemented in **3 languages**:
C, Python, and Rust. The same kind name, the same 5 operations, the
same FNV-1a state hash, the same forecast shape. The substrate is
the only thing that varies.

## The 3 ports

| # | Language | Repo | Target | Real model? | Tests |
|---|---|---|---|---|---|
| 1 | C99 | `quilt-c` | kernel, microcontrollers | stub | 41 |
| 2 | Python | `quilt-timesfm` | workstations, GPU | **real TimesFM 3.0** | 49 |
| 3 | Rust (no_std) | `quilt-timesfm-rust` | embedded (Cortex-M, ESP32) | stub | 49 |

**Total**: 139 tests, 3 languages, bit-exact polyformalism.

## The 4 L-tiers

| Tier | Target | Substrate | RAM |
|---|---|---|---|
| L0 | Cortex-M0+ | synthetic | 4KB |
| L1 | Cortex-M4 | synthetic | 16KB |
| L2 | ESP32-S3 | synthetic | 64KB |
| L3 | Workstation | real TimesFM 3.0 | 1.5GB+ |

The cell at L0 is bit-exact with the cell at L3. Same kind, same
ops, same hash. The substrate is the only thing that varies.

## The FNV-1a test vector

```
FNV-1a("abc") = 0xe71fa2190541574b   ← FIPS 198 test vector
FNV-1a("")    = 0xcbf29ce484222325   ← offset basis
```

These are bit-exact in C, Python, and Rust.

## The 5 operations (bit-exact)

| # | Op | C | Python | Rust |
|---|---|---|---|---|
| 0 | BIND_CONTEXT | `quilt_time_bind_context` | `cell.bind_context` | `cell.bind_context` |
| 1 | BIND_COVARIATE | `quilt_time_bind_covariate` | `cell.bind_past_*_covariate` | `cell.bind_past_*_covariate` |
| 2 | FORECAST | `quilt_time_forecast` | `cell.forecast_` | `cell.forecast` |
| 3 | READ_POINT | `quilt_time_read_point` | `cell.read_point` | `cell.read_point` |
| 4 | READ_QUANTILE | `quilt_time_read_quantile` | `cell.read_quantile` | `cell.read_quantile` |

## The 1-day add workflow

1. Read the C port (30 min)
2. Translate the 5 operations (2 hours)
3. Translate the 5 laws as property tests (1 hour)
4. Implement FNV-1a 64-bit (1 hour)
5. Translate the 9 quantiles and forecast shape (1 hour)
6. Run the 49-test conformance suite (30 min)
7. Push to a new repo, open PR (30 min)

Total: 7 hours. The polyformalism claim is provable in 1 day.

## The polyformalism promise

The promise is not that every cell does the same thing in every
language. The promise is that the **interface** is the same: the
same kind name, the same operation indices, the same state hash,
the same forecast shape. The substrate is the only thing that varies.

**The cell is the system, not the substrate.**

## See also

- Paper F82: The Quilt Time-Cell Visualizer
- Paper F82b: The Quilt Time-Cell on Bare Metal
- Paper F83: The Quilt Time-Cell as a Network Protocol
- `quilt-timesfm/docs/POLYFORMALISM.md`
- `quilt-timesfm-rust/README.md`

---

## Backward derivation (added 2026-08-31, lattice-v2)

Same rule as wiki 18 — polyformalism is opcode-shape:

- **[F0a: The 5 Opcodes](../03-foundations/01-the-5-opcodes.md)** — C and Python agree on kind name, operation indices, FNV-1a state hash, prev-hash PROOF chain: the laws hold across substrates.
- **[C7: The Pinball Loss](../01-calculations/07-pinball-loss.md)** — the substrate varies (stub vs real TimesFM), the forecast object does not; the 9 quantiles are what C7 trains.
