# 23. The Quilt × JEPA World Model

> **Two world models, one cellular architecture.**

This wiki entry explores the synergy between the Quilt `time.cell`
and the JEPA family of world models (V-JEPA 2, I-JEPA, etc.).

## What is JEPA?

**JEPA** (Joint Embedding Predictive Architecture) is a
self-supervised world-model paradigm introduced by Meta AI
(LeCun, 2023). Unlike generative models, JEPA predicts
**embeddings**, not raw outputs.

The architecture:

```
context_x ─→ encoder_x ─┐
                        ├─→ predictor ─→ predicted_y (embedding)
target_y ─→ encoder_y ──┘

loss = ||predictor(encoder_x) - encoder_y||²
       (in embedding space, not output space)
```

## The V-JEPA 2 family

- **V-JEPA 2**: 1.2B video world model, 1M+ hours of video
- **I-JEPA**: image world model
- **A-JEPA**: audio world model
- **M-JEPA**: multi-modal world model

## The 4 roles of the time.cell in a JEPA world model

1. **Compression of JEPA embeddings** — treat 768-d embedding
   stream as a 768-channel multivariate time series.
2. **Uncertainty quantification for JEPA** — 9 quantiles give
   the agent a confidence signal.
3. **Counterfactual reasoning on JEPA states** — "what if the
   world changes?" not just "what if I do?".
4. **Memory of past predictions** — forecasts are durable,
   addressable, learnable semantic objects.

## The 4 use cases

1. **Robotics**: perceive via V-JEPA 2, forecast via time.cell,
   plan via counterfactual reasoning.
2. **Autonomous driving**: perceive via V-JEPA 2, forecast
   trajectories, plan speed/steering.
3. **Video understanding**: predict next scene, forecast 10
   scenes, describe forecast.
4. **Time-series foundation models**: TimesFM 3.0 as a cell
   in the Quilt architecture.

## The 4 future directions

1. **V-JEPA 2 as a substrate** — the time.cell's substrate is
   V-JEPA 2, not TimesFM 3.0.
2. **Cross-modal time cells** — multi-modal temporal primitive.
3. **Hierarchical time cells** — temporal pyramid at multiple
   timescales.
4. **World models as agents** — the world model is an active
   reasoner, not a passive predictor.

## The pivot

The pivot: from "Quilt-TimesFM is a forecasting wrapper" to
"Quilt-TimesFM is a future-state memory primitive for agents".
The 10 capabilities (forecast object, scenarios, counterfactuals,
explainability, lifecycle, memory, decisions, URI, metrics,
CRDT) are the foundation.

## See also

- Paper F87: The Quilt-TimesFM × JEPA Synergy
- Paper F88: The Future-State Memory Pivot
- Paper F89: Counterfactual Reasoning for Agents
- Paper F90: The Agent Utility Metric
- Paper F91: The Temporal Reasoner
- `temporal.py` (this repo): the 10-capability implementation
- `JEPA.md` (this repo): the full JEPA discussion

---

## Honest GAP (noted 2026-08-31, lattice-v2)

The embedding-prediction loss `‖predictor(enc(x)) − enc(y)‖²` needs a metric-geometry rung (least-squares projection in Hilbert space is the small honest candidate). **Not written — open, not faked.** The 2026 ancestor is real and running: elephant's vmf.py/field.py (direction + concentration instead of pixels — see [anchors/world-model-elephant.md](../anchors/world-model-elephant.md)); the uncertainty quantification rides [C7: The Pinball Loss](../01-calculations/07-pinball-loss.md). See [INDEX-V2](../INDEX-V2.md) §2.
