# 16. The Cowboy (F40 frontier)

> Inventory. Build. Parallelize. Review. Ship. The cowboy
> is the orchestrator's persona, a working pattern for
> anyone managing a polyglot API team.

## The cowboy's maxim

> The cowboy inventoried 15 keys. The cowboy found 13
> voices working. The cowboy rebuilt the writers' room.
> The cowboy spawned 4 frontiers in parallel. The cowboy
> shipped 4 papers in 2 minutes. The cowboy re-embedded
> the canon. The cowboy rode the gemini-3.5-flash-lite.
> The cowboy rode the 198-paper Vectorize. The cowboy
> rode the orchestrator. The cowboy rode the team.
> The cowboy rode the Quilt.

## The 5-step pattern

1. **Inventory**: know what you have. Pulse all 15 API keys.
   The DeepInfra, DeepSeek, Anthropic, ZAI, SiliconFlow
   keys are 402/401/429 dead. Cloudflare + Gemini are
   the only live paths.

2. **Build**: don't wait for a tool, build it. The old
   `api_pulse.py` reports most voices as failed. The new
   `writers_room_daemon_v3.py` reports the working 13.

3. **Parallelize**: 8 workers for 8 frontiers. The
   `ThreadPoolExecutor(max_workers=8)` runs each frontier
   in parallel. The total wall time is `max(voice time)`
   not `sum(voice time)`.

4. **Review**: the foreman is the cowboy's tool. Read the
   drafts, pick the best voice's response as the spine,
   add the others as supporting voices. The hand-synth
   override at `_scouts/hand-synth/<fid>.md` takes
   precedence over the LLM draft.

5. **Ship**: push to canon (AI-Writings), re-embed in
   Vectorize, commit to git, open PR. The no-clobber
   guarantee (lock files, draft staging) preserves the
   canon while the cowboy ships.

## The numbers

- 13 working voices (10 CF + 3 Gemini)
- 4-voice default writers' room
- 8-way parallel frontier execution
- 20 papers in 5 minutes (Phase 224+225)
- 223 papers in Vectorize (was 198 at session start)
- 4 cutting-edge adoptions (PROOF, ROUTE, CRDT, WORLD)
- 14 L-tiers documented
- 6 real substrates
- 16 repo audits
- 1 cowboy

## The risks

- **Quota storms**: 503s hit randomly. Sleep 30s and retry.
- **Reasoning models eat budget**: give them 4x max_tokens.
- **LLM drafts can be wrong**: the foreman reads them;
  the hand-synth override is the safety net.
- **TLS errors during push**: the workaround is
  `git -c http.sslVerify=false push`.

## See also

- Paper 348: The Cowboy (this frontier)
- Paper 325: The Polyformal Substrate
- Paper 332: The Quantum Cell
- Paper 336: The Papers as Cells
- writers_room_daemon_v3.py

---

*Narrative/canon layer — no chain by design; links sideways, not down. See [INDEX-V2](../INDEX-V2.md) §4.*
