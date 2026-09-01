# 20. The Time Cell (Phase 228, 5th cutting-edge adoption)

> A time-series foundation model as a Quilt cell. The cell
> value is a forecast with 9 quantile prediction intervals.
> The substrate is Google's TimesFM 3.0 (SOTA on fev-bench,
> TIME, and GIFT-Eval).

## What is a time.cell?

A Quilt cell whose kind is `time.cell`. The cell's state is
a historical time series (a 2D float array). The cell's
value is a forecast (a 2D float array) + 9 quantile
prediction intervals. The cell's reads are covariates
(past-only, past-and-future).

The 5 time-cell operations:

| # | Op | What it does |
|---|---|---|
| 0 | BIND_CONTEXT | Set the historical context (BIND) |
| 1 | BIND_COVARIATE | Set the covariates (BIND) |
| 2 | FORECAST | Run the model (EFFECT) |
| 3 | READ_POINT | Read the point forecast (VIEW) |
| 4 | READ_QUANTILE | Read a quantile prediction interval (VIEW) |

## The substrate: TimesFM 3.0

The cell's evaluator is TimesFM 3.0 (Google Research, Apache 2.0,
~200M parameters, ~800MB on disk). TimesFM 3.0 is rank #1 across
3 major benchmarks:

- **fev-bench**: rank #1 across 100 real-world forecasting tasks
- **TIME Benchmark**: rank #1 across 50 datasets and 98 tasks
- **GIFT-Eval**: rank #1 among all foundation models

It supports:
- Multivariate time series (multiple channels)
- Past-only and past-and-future covariates
- 9 quantile prediction intervals (0.1, 0.2, ..., 0.9)
- 1-16,384 context points
- Both PyTorch and Flax backends

## The polyformalism claim

The cell shape is identical in C and Python:

| Aspect | C (quilt-c) | Python (quilt-timesfm) |
|---|---|---|
| Kind name | "time.cell" | "time.cell" |
| Operations | 5 | 5 |
| Operation indices | 0, 1, 2, 3, 4 | 0, 1, 2, 3, 4 |
| State hash | FNV-1a 64-bit, 4 slices | FNV-1a 64-bit, 4 slices |
| State hash (BIND_CONTEXT) | 32 bytes | 32 bytes |
| prev_hash (PROOF chain) | saved before every BIND | saved before every BIND |
| Forecast point | [horizon, n_variates] | [horizon, n_variates] |
| Forecast quantiles | [9, horizon, n_variates] | [9, horizon, n_variates] |
| Synthetic fallback | hash-seeded -50..+50 | hash-seeded -50..+50 |

The substrate binding is the only thing that varies:
- C: stub (synthetic, no model)
- Python: real TimesFM 3.0 (when torch is available), stub fallback

## The 11 opcodes

The Quilt opcodes are now:

```
BIND / LINK / EFFECT / VIEW / TICK / FORGET
(5)                                 (+1)
PROOF / ROUTE / CRDT / WORLD / TIME
(+1 cutting-edge #1) (+1 #2) (+1 #3) (+1 #4) (+1 #5)
```

The 5 laws (BIND idempotence, LINK transitivity, EFFECT
associativity, VIEW purity, TICK monotonicity, FORGET
completeness) are unchanged. TIME inherits BIND/EFFECT/VIEW
semantics and adds nothing new to the law set.

## The use cases

- **Financial forecasting**: revenue, stock prices, demand
- **Sensor monitoring**: temperature, pressure, vibration
- **Web analytics**: page views, DAU, conversion rates
- **Healthcare**: patient vitals, lab results
- **Energy**: load, generation, demand
- **Scientific**: weather, climate, telemetry
- **Operations**: inventory, supply chain, logistics

All without training a custom model. The cell is the model.

## The benchmarks

| Benchmark | TimesFM 3.0 | Previous SOTA |
|---|---|---|
| fev-bench (100 tasks) | rank #1 | ? |
| TIME (98 tasks) | rank #1 | ? |
| GIFT-Eval (foundation) | rank #1 | ? |

## The math

The model uses a patch-based transformer:
- input_patch_length = 32
- output_patch_length = 64 (the horizon)
- 9 quantiles per output token
- RevIN (Reversible Instance Normalization) for distribution shift

The training loss: a quantile regression loss:

L_q = max(q * (y - y_pred), (q-1) * (y - y_pred))

for each quantile q. The 9 quantiles are predicted jointly.

## Backward derivation (added 2026-08-31, lattice-v2)

- **[C7: The Pinball Loss](../01-calculations/07-pinball-loss.md)** — the quantile loss above is Koenker & Bassett 1978, REAL math, now with its own rung: the 9 intervals are what the asymmetry trains
- **[F0a: The 5 Opcodes](../03-foundations/01-the-5-opcodes.md)** — the 5 time-cell operations (BIND_CONTEXT/BIND_COVARIATE/FORECAST/READ_POINT/READ_QUANTILE) are BIND/BIND/EFFECT/VIEW/VIEW — polyformalism is opcode-shape, so the chain terminates at the canon honestly
- **GAP (honest):** the patch-transformer architecture itself (RevIN, patching) has no mathematics rung here. That is 2026 substrate engineering, not 2126 derivation — marked open, not faked.

## See also

- Paper 385: The Time Cell
- Paper 386: The Time Cell Beats Proprietary Models
- Paper 387: The Time Substrate
- Paper 388: The Time Cell's Math
- Paper 389: The Time Cell as CRDT
- Paper 390: The Time Cell's PROOF Chain
- quilt-c/include/quilt/time.h
- quilt-c/src/time.c
- quilt-c/tests/test_time.c (41 tests)
- quilt-timesfm/quilt_cell.py
- quilt-timesfm/tests/test_quilt_cell.py (45 tests)
- github.com/SuperInstance/quilt-timesfm
