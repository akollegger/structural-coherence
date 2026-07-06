# RFC-008 — Structured Memory Over Task Horizon (Agentic Memory)

**Status:** Awaiting RFC. `proposals/RFC-008-agentic-memory-horizon.md` has not been written yet.
**Source:** RFC-001 §8.6 (and §8.6.1 for the prior-art requirement below).

## Scope

The flagship experiment: the most direct test of the framework's central thesis, because
it operationalizes volume as *task horizon* and supplies a known-in-advance critical
volume $V_c$ — the context window — rather than one recoverable only by fitting.

Hold agent and task distribution fixed; vary memory architecture along a ladder mirroring
RFC-001 §§4, 6: (i) unstructured append-only log, (ii) embedding-based retrieval (RAG),
(iii) schema-structured memory (typed entities/relations), (iv) graph memory with
community/motif structure. Sweep task horizon across and beyond the context-window
boundary. Measure coherence *behaviorally* (self-contradiction rate, superseded-belief
actions, constraint retention) rather than by counting contradictions in the store.

Two design requirements are non-negotiable per RFC-001 §8.6:
1. Match retrieval budget across conditions.
2. Report self-consistency separately from task-success, to isolate the coherence-maintenance
   effect from a plain retrieval-quality effect.

## Prior-art requirement (§8.6.1)

RFC-001 explicitly withholds a firm claim of novelty here and leaves a placeholder: before
this RFC can be frozen, survey long-context/long-horizon agent benchmarks, memory-augmented
agent architectures, and self-consistency/contradiction metrics already in use, and confirm
the context-window-as-$V_c$ framing and the self-consistency/task-success split aren't
already occupied. Write that survey to `prior-art.md` in this folder — it's a precondition
for the RFC, not an afterthought once results are in.

## Layout

- `prior-art.md` — literature survey resolving §8.6.1 (write this before the RFC is frozen).
- `data/` — task set, memory-architecture implementations, horizon schedule.
- `src/` — agent harness, per-architecture memory adapters, self-consistency/task-success instrumentation.
- `results/` — `RESULTS.md` verdict plus `figures/`.

## Before running

Freeze `proposals/RFC-008-agentic-memory-horizon.md` first — and freeze it only after
`prior-art.md` exists and has been reviewed, per the requirement above.
