# RFC-003 — Enrichment-Only Noise Amplification

**Status:** Awaiting RFC. `proposals/RFC-003-enrichment-noise-amplification.md` has not been written yet.
**Source:** RFC-001 §8.4.

## Scope

Instrument a vector-retrieval pipeline to attribute precision loss to contradiction among
near-neighbors as a function of corpus volume $V$, and test whether adding a dampening
layer (constraint-based prefilter) recovers precision as predicted — the concrete test of
RFC-001 §4.1's claim that enrichment-dominant structure (embeddings) amplifies rather than
suppresses inconsistency.

## Layout

- `data/` — corpus and embedding model choice, growth schedule.
- `src/` — retrieval pipeline instrumentation, contradiction attribution, dampening-layer ablation.
- `results/` — `RESULTS.md` verdict plus `figures/`.

## Before running

Freeze `proposals/RFC-003-enrichment-noise-amplification.md` first — it needs to specify
the embedding model, the corpus/growth schedule, how "attributed precision loss" is
computed, and the specific dampening layer used for the recovery test.
