# ANCHOR — The World Model ← elephant (vmf.py, field.py)

*The Quilt × JEPA World Model (wiki 23) and the Time Cell (wiki 20), anchored to their real 2026 seed.*

## The 2026 seed

- **`elephant`** (`/home/eileen/projects/elephant`) — the fleet's world-model mathematics, in two files:
  - **`elephant/vmf.py`** — von Mises–Fisher MLE: a room's state as a *direction* μ̂ with concentration κ, solved by Newton's method with a closed-form half-integer Bessel ratio. Cold room = high κ (tight, one way to be); warm room = low κ (loose, many ways to be). Guards that are the wiki's honesty doctrine in compiled form: κ = None under N < 10 ("not identifiable, never a fake number"), ρ clamped, jackknife SE as the drift deadband.
  - **`elephant/field.py`** — the RoomField: 7 dials (mood, volume, earnestness, cynicism, joke_landing, panic, presence), the ensemble as the room's temperature. "A room is not its messages."

## What exists

Predict-the-field-not-the-pixels, in production shape: direction + concentration as sufficient statistics, standardized dial spaces, bootstrap CIs. This is JEPA's wager — predict in embedding/latent space, not output space — already running on 7 honest dimensions instead of 768.

## The gap to 2126

- wiki 23's counterfactual reasoning, scenario objects, agent-utility metrics: design, not code.
- The JEPA embedding loss `‖predictor(enc(x)) − enc(y)‖²` has no mathematics rung in this wiki (GAP, named in [INDEX-V2](../INDEX-V2.md)); elephant's vMF machinery is the natural candidate for that rung — κ-as-uncertainty is the 2026 ancestor of the 9-quantile forecast ([C7](../01-calculations/07-pinball-loss.md)).

> The wiki says the world model predicts embeddings. The 2026 seed predicts a direction and a concentration — the whole elephant in seven dials, never a fake number.
