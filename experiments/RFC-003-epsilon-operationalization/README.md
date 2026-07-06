# RFC-003 — Operationalizing ε, and Coherence Decay Under Fixed Structure

**Status:** Awaiting RFC. `proposals/RFC-003-epsilon-operationalization.md` has not been written yet.
**Source:** RFC-001 §8.1.

## Scope

Before any decay curve can be fit, inconsistency ($\epsilon$) needs a concrete, reproducible
operational definition — RFC-001 §3.1.1 flags this as an open measurement problem, not a
settled one. This experiment folder covers both: pinning down $\epsilon$, and then measuring
whether a corpus held at fixed structural complexity $S$ shows the predicted $V^{-\beta}$
coherence decay.

This is the foundational experiment in the program — RFC-004 and RFC-005 both depend on
whatever operational choices are made here.

## Layout

- `data/` — corpus construction/sampling and its documentation.
- `src/` — contradiction-scoring pipeline (NLI/cross-encoder), curve fitting.
- `results/` — `RESULTS.md` verdict plus `figures/`.

## Before running

Do not start data collection until `proposals/RFC-003-epsilon-operationalization.md` is
frozen — it needs to pin down the specific $\epsilon$-definition(s) under test, the corpora
or corpus-construction method, the task-based measure of $I$, and the model-comparison
criterion for the curve fit (see RFC-001 §8, opening paragraph, for what's still missing).
