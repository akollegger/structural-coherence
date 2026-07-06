# RFC-002 — The Semantic Layer as Restored Dampening (Text-to-SQL)

**Status:** RFC drafted, not yet frozen — `proposals/RFC-002-semantic-layer-text-to-sql.md`
is a pre-registration draft (v3) with an explicit end-of-document placeholder list of
design decisions (domain/warehouse, schema-volume rungs, denormalization-degree metric
weights, question inventory, model/judge configuration, analysis plan) still to commit
before a run.
**Source:** RFC-001 §8.7.
**Note:** This is the first experiment specified in full under the RFC-001 program,
numbered RFC-002 by the author out of §8 order — it was chosen first because the
prior-art base (semantic-layer/text-to-SQL literature) is strong enough to build on
rather than construct from scratch. It does not depend on, and is not depended on by,
RFC-003 through RFC-008 (the §8.1–8.6 experiments).

## Scope

Tests RFC-001's claim that denormalization is a deliberate lowering of dampening ($\sigma$)
at the physical-schema layer, and that a semantic layer is a priori compound structure at
the query/physical seam that restores it — predicting a text-to-SQL accuracy dose-response
against denormalization degree, and a naming ladder (appropriate → consistent → conventional
→ explicit declaration) that separates interpretation relief from restored dampening and
enrichment.

Six falsifiable predictions (P1–P6) are pre-registered in the RFC, crossing two axes
(schema volume, swept exponentially, and denormalization degree, D0–D3) against a
cumulative five-rung context ladder (C0–C4). See the RFC's §3 and §5 ("What each outcome
would mean for RFC-001") for the full prediction set and how each possible result maps
back onto the framework.

## Layout

- `data/` — the source warehouse/domain, the denormalization sweep (D0–D3), the
  schema-volume rungs, and the per-rung (C0–C4) naming/declaration documents.
- `src/` — harness for running the model × schema-version × context-rung grid,
  execution-based grading, and the pre-registered analysis (monotonicity tests, the
  power-law-vs-linear fit for P5, the composite-vs-single-axis comparison for P6).
- `results/` — `RESULTS.md` verdict plus `figures/`.

## Before running

Freeze `proposals/RFC-002-semantic-layer-text-to-sql.md` first. Per its own placeholder
list (end of document) and Section 6 ("Threats to validity"), that means committing:
the specific domain/source warehouse, the schema-volume rungs and scaling method that
holds the answerable-question set fixed, the denormalization-degree metric's weights,
the per-class question inventory, model versions and effort settings, judge configuration
plus human-audit sampling — and, most importantly, having a blind rater confirm the C0–C4
rung documents differ *only* in their intended mechanism (Section 6's central validity
threat) before any model is run.
