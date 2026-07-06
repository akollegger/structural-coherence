# RFC Index

Status of every RFC in this repo. Update this table in the same commit as any RFC or
experiment-status change.

| RFC | Title | Status | RFC-001 § | Experiment folder |
|-----|-------|--------|-----------|--------------------|
| [RFC-001](RFC-001-resonance-structure-coherence.md) | Resonance: A Descriptive Account of How Latent Structure Keeps Growing Information Coherent | Frozen argument (v7); §8 extending | — | — |
| [RFC-002](RFC-002-semantic-layer-text-to-sql.md) | The Semantic Layer as Restored Dampening: A Test of the Resonance Framework on Text-to-SQL | Draft (v3) | §8.7 | [`experiments/RFC-002-semantic-layer-text-to-sql/`](../experiments/RFC-002-semantic-layer-text-to-sql/) |
| RFC-003 | Operationalizing ε, and coherence decay under fixed structure | Not started | §8.1 | [`experiments/RFC-003-epsilon-operationalization/`](../experiments/RFC-003-epsilon-operationalization/) |
| RFC-004 | Leverage growth and the phase boundary | Not started | §8.2 | [`experiments/RFC-004-leverage-phase-boundary/`](../experiments/RFC-004-leverage-phase-boundary/) |
| RFC-005 | The scaling exponents δ and γ, and their trajectories | Not started | §8.3 | [`experiments/RFC-005-scaling-exponents/`](../experiments/RFC-005-scaling-exponents/) |
| RFC-006 | Enrichment-only noise amplification | Not started | §8.4 | [`experiments/RFC-006-enrichment-noise-amplification/`](../experiments/RFC-006-enrichment-noise-amplification/) |
| RFC-007 | The programming-language gradient | Not started | §8.5 | [`experiments/RFC-007-typescript-migration-gradient/`](../experiments/RFC-007-typescript-migration-gradient/) |
| RFC-008 | Structured memory over task horizon (agentic memory) | Not started | §8.6 | [`experiments/RFC-008-agentic-memory-horizon/`](../experiments/RFC-008-agentic-memory-horizon/) |

## Status legend

- **Not started** — no RFC file yet.
- **Draft** — RFC file exists, still being written (open effect sizes, null models, etc.).
- **Frozen** — RFC is complete and stable; edits happen only via an appended version-history entry, per RFC-001's own convention.
- **Running** — the linked experiment is actively executing against a frozen RFC.
- **Complete** — `results/RESULTS.md` in the linked experiment folder has a verdict.

## Numbering note

RFC numbers are assigned in the order RFCs are written, not in RFC-001 §8's section
order. RFC-002 (§8.7) was written first among the experiments because its prior-art base
is strong enough to build on directly; RFC-003–008 cover §8.1–8.6 in section order. When
a new experimental RFC is added, append it at the next free number regardless of which
§8.N it targets, and update this table.

## Sequencing note

RFC-002 is independent of the others — it doesn't depend on, and isn't depended on by,
RFC-003–008. Within the §8.1–8.6 group: RFC-003 is foundational (it operationalizes
$\epsilon$) and RFC-004 depends on RFC-005's exponent estimates for its sharper test.
RFC-006, RFC-007, and RFC-008 are independent of one another and of the above. RFC-008
additionally requires its `prior-art.md` survey before it can be frozen (RFC-001 §8.6.1),
and RFC-002 requires its own end-of-document design decisions (domain, schema-volume
rungs, denormalization metric weights, question inventory, etc.) to be committed first.
