# 26: The Playtest Workflow — From API to Improvement

## Overview

This document specifies the external playtest workflow utilized to verify `quilt-timesfm` and associated control systems against empirical data. This workflow governs execution, quantitative capture, baseline comparison, automated auditing, iterative remediation, paper generation, and vector indexing.

---

## The Playtest Pipeline

The verification procedure executes through nine sequential stages:

1. **End-to-End Execution**: Run the target application on unmasked, real-world data sources.
2. **Metric Capture**: Record all telemetry, specifically P&L, error rates, and system latency.
3. **Baseline Comparison**: Benchmark captured metrics against defined historical or theoretical baselines.
4. **Automated LLM Grading**: Dispatch output artifacts to LLM APIs for structural, mathematical, and narrative auditing.
5. **Bug Isolation**: Identify code defects, edge-case failures, and performance bottlenecks flagged by the audit.
6. **Iteration**: Patch identified code segments, re-execute the test harness, and re-run grading.
7. **Documentation**: Compile verified findings into a formalized Quilt technical paper.
8. **Vector Embedding**: Process generated documents via `re_embed_v2.py` for indexing in Vectorize.
9. **Version Control**: Commit artifacts and push state to GitHub.

---

## Execution Environment & Tooling

The verification pipeline relies on a standardized local and daemonized toolchain:

* **Execution Core**: `bash`, `python3`
* **Cross-Repo Audit**: `/workspace/_scouts/quick_audit.py`
* **Benchmark Harness**: `/workspace/_scouts/compare_controllers.py`
* **Grading Daemon**: `writers_room_daemon_v3.py` (interfaces with Cloudflare and Gemini APIs)
* **Vector Indexing**: `re_embed_v2.py`

---

## Documented Playtest Runs (September 2026)

### Playtest 1: Multi-Asset Equity (5-Year Horizon)

* **Assets**: AAPL, MSFT, GOOGL, TSLA, SPY, QQQ (6 total)
* **Time Period**: 2020-01-01 to 2024-12-31
* **Data Source**: Yahoo Finance ingested via raw `urllib` calls.
* **Execution Parameters**: 5 basis points (0.05%) applied per transaction.
* **Quantitative Results**: 
  * All 6 assets yielded positive cumulative returns.
  * Average cumulative return: +193% over the 5-year period.
* **Identified Defects (4)**:
  1. Volatility threshold miscalibration.
  2. Incorrect $\sqrt{t}$ scaling applied to confidence intervals.
  3. Missing property in state serialization.
  4. Runtime type-check failure on float-to-integer conversion.

---

### Playtest 2: Regime Stress-Testing

* **Time Periods**: 
  * Regime A: 2007–2010 (Global Financial Crisis)
  * Regime B: 2010–2024 (Post-Crisis Recovery & Bull Market)
* **Quantitative Results**:
  * Strategy classification verified as risk-mitigation rather than return-maximization.
  * **2008 Drawdown Benchmark**: SPY Trader variant recorded a -0.46% return, compared to -11.1% for Buy & Hold (B&H) over the identical stress window.

---

### Robotics Control Playtest

* **Controllers Tested**: PD, PID, LQR, Cell-driven
* **Test Parameters**: 2000-tick constant target setpoint.
* **Quantitative Results (Performance Hierarchy)**: 
  * Cell-driven > LQR > PID > PD
  * The Cell-driven controller achieved a 100% performance improvement over the LQR baseline in settling time and steady-state error reduction.

---

## LLM Grading Integration

Automated evaluation runs via Cloudflare and Gemini API integrations (`writers_room_daemon_v3.py`) perform three core validation functions:

1. **Gap Analysis**: Detects missing methodological metrics in the output (e.g., maximum drawdown, slippage impact, walk-forward validation splits).
2. **Defect Detection**: Flags latent code bugs (e.g., calibration thresholds, type coercion errors) prior to manual review.
3. **Narrative Verification**: Audits empirical claims against raw logs to confirm alignment between system behavior and documented conclusions (e.g., confirming the risk-management profile observed in Playtest 2).

---

## Summary

The `quilt-timesfm` playtest workflow enforces rigorous, data-driven validation of stochastic and control models. By pairing deterministic execution—such as 5-year multi-asset backtests and 2000-tick robotics simulations—with automated LLM grading via Cloudflare and Gemini APIs, the system systematically surfaces code defects, quantifies risk-mitigation properties (such as the 2008 SPY drawdown reduction from -11.1% to -0.46%), and ensures continuous documentation hygiene through automated Vectorize embedding and GitHub synchronization.