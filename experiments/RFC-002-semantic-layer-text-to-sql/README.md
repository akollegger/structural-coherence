# RFC-002 — The Semantic Layer as Restored Dampening (Text-to-SQL)

**Status:** RFC frozen for execution — `proposals/RFC-002-semantic-layer-text-to-sql.md`
is v4. Domain, warehouse, grid size, model design, judge configuration, and the full
analysis plan are all committed; what remains is implementation (literal DDL, question
text, and the specific model pair), not design.
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

## Committed design (RFC v4)

- **Domain/warehouse:** synthetic, Contoso-inspired retail dataset, built from twelve
  business modules, in DuckDB (§4.5 of the RFC).
- **Grid:** a budget-scoped pilot — 4 volume rungs ($2, 8, 32, 128$) × 4 denorm degrees ×
  5 context rungs × 24 core questions × 2 models = 3,840 graded completions.
- **Models:** two models from one provider spanning capability tiers; literal identity
  deferred to actual API access at build time (§4.3).
- **Judge:** same-provider automated judge + human audit (10% stratified sample, plus
  every analytical/strict disagreement) substituting for cross-family judging (§4.4).
- **Analysis:** a mixed-effects logistic regression as the primary framework for P1–P4,
  with AIC/BIC and cross-validated log-loss model comparisons for P5/P6 (§8).

## Layout

- `data/` — the source warehouse/domain, the denormalization sweep (D0–D3), the
  schema-volume rungs, and the per-rung (C0–C4) naming/declaration documents.
- `src/` — harness for running the model × schema-version × context-rung grid,
  execution-based grading, and the pre-registered analysis (monotonicity tests, the
  power-law-vs-linear fit for P5, the composite-vs-single-axis comparison for P6).
- `results/` — `RESULTS.md` verdict plus `figures/`.

## Before running

The RFC is frozen — implementation can start. Per §4.5 and §6 ("Threats to validity"),
build in this order:

1. Generate the twelve-module Contoso-inspired retail domain at each of the four
   schema-volume rungs, each in D0–D3 denormalized form, in DuckDB.
2. Author the fixed 24-question core inventory (4 questions × 6 error classes) against
   the smallest ($V{=}2$) schema, with reference SQL.
3. Author the C0–C4 context documents per rung from a single shared term inventory, and
   have a blind rater confirm each rung differs *only* in its intended mechanism (§6's
   central validity threat) before any model is run — this gates the run, not an
   afterthought.
4. Confirm the actual model pair (two tiers, one provider) against real API access, and
   record it here, in `data/README.md`, before running.
5. Wire up the automated judge and the human-audit sampling plan (§4.4).
6. Implement the §8 analysis pipeline against a dry run before the real one, so the fit
   code is validated before it matters.
