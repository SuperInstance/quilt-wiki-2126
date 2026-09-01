# 21. The Time-Cell Visualizer

> **A live, in-browser cell-graph explorer for the `time.cell` kind.**

The Quilt `time.cell` is the most important cell kind since the
original 5 opcodes. The visualizer makes the cell graph *visible*.

## The 5 design principles

1. **Decompose every operation into cell operations**
2. **Animate the cell graph in real-time**
3. **Walk through a recorded session**
4. **Compare the polyformalism ports**
5. **Be self-contained** (vanilla HTML + Canvas + JS, no build)

## The cell graph (5 nodes, 4 edges)

```
context    →   forecast
covariate  →   forecast
forecast   →   point
forecast   →   quantile
```

## The PROOF chain animation

Every BIND_CONTEXT saves prev_hash → state_hash. The visualizer
animates this as a "chain link" between the old and new hashes.

## The abductive loop

The FORECAST operation is an abductive loop: PROPOSE → EXECUTE →
RENDER → VERIFY → REFINE. The visualizer animates all 5 sub-operations
as colored flashes on the forecast cell.

## The polyformalism panel

Side-by-side C, Python, Rust. Same kind, same hash, same forecast
shape. The user can verify bit-exactness by hashing the same context
in all 3 ports.

## The 6 context patterns

- Sine wave
- Linear trend
- Random walk
- Step function
- Seasonal (year + week)
- Real data (trend + sine + noise)

## The file

`quilt-timesfm/visualizer/index.html` — 33KB, vanilla HTML +
Canvas + JS. No build step. No dependencies. Just open the file.

## The 4 use cases

1. **Teaching Quilt**: 5-minute intuition for the cell model
2. **Debugging a forecast**: replay a context, see where the cell diverges
3. **Comparing the polyformalism**: verify C, Python, Rust are bit-exact
4. **Designing a new cell kind**: see how the time.cell graph is structured

## See also

- Paper F82: The Quilt Time-Cell Visualizer
- README in quilt-timesfm (Section: "Interactive visualizer")
