# RFC-006 — Operationalizing ε, and Coherence Decay Under Fixed Structure

**Status:** Awaiting RFC. `proposals/RFC-006-epsilon-operationalization.md` has not been written yet.
**Source:** RFC-001 §8.1.

## Scope

Before any decay curve can be fit, inconsistency ($\epsilon$) needs a concrete, reproducible
operational definition — RFC-001 §3.1.1 flags this as an open measurement problem, not a
settled one. This experiment folder covers both: pinning down $\epsilon$, and then measuring
whether a corpus held at fixed structural complexity $S$ shows the predicted $V^{-\beta}$
coherence decay.

This is deliberately sequenced *after* RFC-002 through RFC-005 rather than first: those
four domain experiments (semantic-layer/text-to-SQL, enrichment/embeddings, agentic
memory, code) each have mature prior art and are likely to surface a working,
domain-tested $\epsilon$ proxy (execution-based SQL correctness, near-neighbor
contradiction, self-consistency metrics, defect density) as a byproduct. This RFC should
synthesize those proxies rather than inventing an operationalization cold. RFC-008 and
RFC-007 both depend on whatever operational choices are made here.

## Layout

- `data/` — corpus construction/sampling and its documentation.
- `src/` — contradiction-scoring pipeline (NLI/cross-encoder), curve fitting.
- `results/` — `RESULTS.md` verdict plus `figures/`.

## Before running

Do not start data collection until `proposals/RFC-006-epsilon-operationalization.md` is
frozen — it needs to pin down the specific $\epsilon$-definition(s) under test, the corpora
or corpus-construction method, the task-based measure of $I$, and the model-comparison
criterion for the curve fit (see RFC-001 §8, opening paragraph, for what's still missing).
Draft this RFC only after reviewing what RFC-002/003/004/005 actually used as their
domain-specific inconsistency proxies.
