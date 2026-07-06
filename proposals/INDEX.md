# RFC Index

Status of every RFC in this repo. Update this table in the same commit as any RFC or
experiment-status change.

| RFC | Title | Status | RFC-001 § | Experiment folder |
|-----|-------|--------|-----------|--------------------|
| [RFC-001](RFC-001-resonance-structure-coherence.md) | Resonance: A Descriptive Account of How Latent Structure Keeps Growing Information Coherent | Frozen (v4) | — | — |
| RFC-002 | Operationalizing ε, and coherence decay under fixed structure | Not started | §8.1 | [`experiments/RFC-002-epsilon-operationalization/`](../experiments/RFC-002-epsilon-operationalization/) |
| RFC-003 | Leverage growth and the phase boundary | Not started | §8.2 | [`experiments/RFC-003-leverage-phase-boundary/`](../experiments/RFC-003-leverage-phase-boundary/) |
| RFC-004 | The scaling exponents δ and γ, and their trajectories | Not started | §8.3 | [`experiments/RFC-004-scaling-exponents/`](../experiments/RFC-004-scaling-exponents/) |
| RFC-005 | Enrichment-only noise amplification | Not started | §8.4 | [`experiments/RFC-005-enrichment-noise-amplification/`](../experiments/RFC-005-enrichment-noise-amplification/) |
| RFC-006 | The programming-language gradient | Not started | §8.5 | [`experiments/RFC-006-typescript-migration-gradient/`](../experiments/RFC-006-typescript-migration-gradient/) |
| RFC-007 | Structured memory over task horizon (agentic memory) | Not started | §8.6 | [`experiments/RFC-007-agentic-memory-horizon/`](../experiments/RFC-007-agentic-memory-horizon/) |

## Status legend

- **Not started** — no RFC file yet.
- **Draft** — RFC file exists, still being written (open effect sizes, null models, etc.).
- **Frozen** — RFC is complete and stable; edits happen only via an appended version-history entry, per RFC-001's own convention.
- **Running** — the linked experiment is actively executing against a frozen RFC.
- **Complete** — `results/RESULTS.md` in the linked experiment folder has a verdict.

## Sequencing note

RFC-002 is foundational (it operationalizes $\epsilon$) and RFC-003 depends on RFC-004's
exponent estimates for its sharper test. RFC-005, RFC-006, and RFC-007 are independent of
one another and of the above. RFC-007 additionally requires its `prior-art.md` survey
before it can be frozen (RFC-001 §8.6.1).
