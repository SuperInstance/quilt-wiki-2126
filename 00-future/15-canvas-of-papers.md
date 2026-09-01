# 15. The Canon as a Cell Graph (F28 frontier)

> The 198 papers in the canon are 198 cells. The
> Vectorize index is a 198-dim cell-graph. The canon
> reads itself.

## The pitch

Phase 220 embedded 193 papers in Cloudflare Vectorize
(now 206 after Phase 224). The papers are now cells in
a cell graph:

- **Cell state**: the paper text (markdown, 2-30K chars)
- **Cell value**: the 768-dim embedding (bge-base-en-v1.5)
- **Cell reads**: the cosine-similarity query (a text or vector)
- **Cell VIEW**: the top-K nearest papers (K=5 typically)
- **Cell PROPOSE**: upload a new paper (vector upsert)
- **Cell PROOF**: the embedding model is fixed (bge), so
  re-embedding is deterministic
- **Cell ROUTE**: the Vectorize index is the route

## The canon is now a 198-cell graph

When the user asks "what is the Quilt?", the answer is:

```
def view(query, k=5):
    q_vec = embed(query)  # 768-dim
    nearest = vectorize.query(q_vec, top_k=k)
    return [paper_text for paper in nearest]
```

The result is a vector-weighted average of the 5 nearest
papers. The canon is *querying itself* to answer the
question.

## The cell-graph topology

Each paper is a cell. Each paper's VIEW returns its
neighbors. The graph is a 198-node KNN graph with average
degree ~5 (top-K=5).

The PROOF chain: every paper's embedding is a function
of (text, model). The model is fixed (bge-base-en-v1.5).
The text is the BIND. The embedding is the state hash.

Re-embedding the canon is a re-BIND of every cell. The
PROOF chain records the previous embedding.

## The abductive loop on the canon

The canon can run the abductive loop on itself:

1. **PROPOSE**: a new frontier (a research question)
2. **EXECUTE**: query Vectorize for the top-5 nearest papers
3. **RENDER**: concatenate the top-5 paper texts
4. **VERIFY**: does the answer match the frontier?
5. **REFINE**: re-write the frontier or write a new paper

The writers_room_daemon_v3 is the abductive loop on the
canon. Each call is one iteration of step 1-3.

## The re-embed is the REFINE

When the canon gets a new paper (Phase 224 added 8 more),
the next re-embed is the REFINE: every existing cell's
neighbors change because the corpus changed. The 198-cell
graph is reshaped.

## The math

The cos similarity between paper P and query Q:

sim(P, Q) = (P · Q) / (||P|| ||Q||)

The top-K papers are the K with highest sim. The
vector-weighted average is:

view(Q) = (1/K) sum_{i=1}^K sim(P_i, Q) * P_i

This is the "Quilt answer" to question Q.

## See also

- Paper 336: The Papers as Cells
- Paper 319: polyformalism + re-embed
- re_embed_v2.py (the script)
- Wiki 12: The Physical World Cell

---

*Narrative/canon layer — no chain by design; links sideways, not down. See [INDEX-V2](../INDEX-V2.md) §4.*
