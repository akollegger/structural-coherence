# Prior Art Survey — RFC-008 (resolves RFC-001 §8.6.1)

**Status:** Not yet written.

RFC-001 §8.6.1 names four areas to survey before this experiment's RFC can be frozen:

1. Long-context and long-horizon agent benchmarks.
2. Memory-augmented agent architectures and their published evaluations.
3. Self-consistency and contradiction-detection metrics already in use for dialogue and
   long-form generation.
4. Any existing work that varies memory structure while holding the agent fixed.

RFC-001 §11's reference list already names one directly relevant benchmark to position
against: *AMA-Bench: Evaluating Long-Horizon Memory for Agentic Applications* (2026),
which uses causality-graph-based memory.

The distinguishing contribution to defend here is narrow and specific: the use of the
context-window boundary as a *predicted* $V_c$ (known in advance, not fit after the
fact), and the separation of self-consistency from task-success to isolate
coherence-maintenance from retrieval quality. Confirm neither is already covered before
proceeding.
