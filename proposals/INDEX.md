# RFC Index

Status of every RFC in this repo. Update this table in the same commit as any RFC or
experiment-status change.

| RFC | Title | Status | RFC-001 § | Experiment folder |
|-----|-------|--------|-----------|--------------------|
| [RFC-001](RFC-001-resonance-structure-coherence.md) | Resonance: A Descriptive Account of How Latent Structure Keeps Growing Information Coherent | Frozen argument (v7); §8 extending | — | — |
| [RFC-002](RFC-002-semantic-layer-text-to-sql.md) | The Semantic Layer as Restored Dampening: A Test of the Resonance Framework on Text-to-SQL | Frozen (v4) | §8.7 | [`experiments/RFC-002-semantic-layer-text-to-sql/`](../experiments/RFC-002-semantic-layer-text-to-sql/) |
| RFC-003 | Enrichment-only noise amplification | Not started | §8.4 | [`experiments/RFC-003-enrichment-noise-amplification/`](../experiments/RFC-003-enrichment-noise-amplification/) |
| RFC-004 | Structured memory over task horizon (agentic memory) | Not started | §8.6 | [`experiments/RFC-004-agentic-memory-horizon/`](../experiments/RFC-004-agentic-memory-horizon/) |
| RFC-005 | The programming-language gradient | Not started | §8.5 | [`experiments/RFC-005-typescript-migration-gradient/`](../experiments/RFC-005-typescript-migration-gradient/) |
| RFC-006 | Operationalizing ε, and coherence decay under fixed structure | Not started | §8.1 | [`experiments/RFC-006-epsilon-operationalization/`](../experiments/RFC-006-epsilon-operationalization/) |
| RFC-007 | The scaling exponents δ and γ, and their trajectories | Not started | §8.3 | [`experiments/RFC-007-scaling-exponents/`](../experiments/RFC-007-scaling-exponents/) |
| RFC-008 | Leverage growth and the phase boundary | Not started | §8.2 | [`experiments/RFC-008-leverage-phase-boundary/`](../experiments/RFC-008-leverage-phase-boundary/) |

## Status legend

- **Not started** — no RFC file yet.
- **Draft** — RFC file exists, still being written (open effect sizes, null models, etc.).
- **Frozen** — RFC is complete and stable; edits happen only via an appended version-history entry, per RFC-001's own convention.
- **Running** — the linked experiment is actively executing against a frozen RFC.
- **Complete** — `results/RESULTS.md` in the linked experiment folder has a verdict.

## Numbering note

RFC numbers reflect the program's recommended execution order — domain-literature
maturity first, cross-domain synthesis last — not RFC-001 §8's section order and not
strict write order. RFC-002 (§8.7) is first because it's already drafted and leans on an
established literature. When a new experimental RFC is added or the plan is
re-sequenced, renumber to keep this property true, update every experiment folder's name
and internal cross-references, and update this table.

## Sequencing note (rationale)

The program is deliberately ordered to let domain experiments with strong prior art
surface working $\epsilon$ candidates *before* committing to an operationalization in the
abstract:

1. **RFC-002** — semantic layer / text-to-SQL. Frozen (v4): domain (synthetic
   Contoso-inspired retail), warehouse (DuckDB), grid size (a budget-scoped 4-rung
   pilot), model design (2 models, 1 provider), judge config, and the full analysis plan
   are all committed. Yields a hard, execution-based inconsistency proxy (SQL
   correctness / error taxonomy). Ready for implementation.
2. **RFC-003** — enrichment-only noise amplification (embeddings/retrieval). RFC-001's
   own first motivating example (§2); yields a soft, similarity-based proxy
   (near-neighbor contradiction).
3. **RFC-004** — agentic memory horizon. The flagship; soft inconsistency is the
   *operative* quantity here per RFC-001 §3.1.1. Highest build cost (multi-architecture
   agent harness) and gated on its own §8.6.1 prior-art survey — sequenced third so its
   design can borrow measurement instincts from RFC-002/003.
4. **RFC-005** — TS/JS migration gradient. RFC-001 itself calls this "the program's
   hardest empirical lift" (heaviest confounds); its proxy (defect density) is the most
   indirect. Last among the domain experiments.
5. **RFC-006** — epsilon operationalization. Synthesizes whatever proxies actually
   worked across RFC-002–005, rather than inventing one cold. Depends on 002–005.
6. **RFC-007** — scaling exponents δ, γ. Its own method calls for "natural corpora
   across domains" — check whether this becomes a meta-analysis over the RFC-002–005
   datasets rather than fresh data collection. Depends on RFC-006's epsilon choice.
7. **RFC-008** — leverage growth / phase boundary. Depends on RFC-007's exponents; last.

RFC-008 additionally needs RFC-007; RFC-007 needs RFC-006; RFC-006 needs RFC-002–005.
RFC-004 additionally requires its `prior-art.md` survey before it can be frozen
(RFC-001 §8.6.1).
