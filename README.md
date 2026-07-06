# structural-coherence

An RFC-driven research program around **RFC-001: "Resonance"** — a formal framework for
how information architecture must scale with data volume to stay coherent. This repo holds
the framework, the experiments proposed to test it, and their results.

## Layout

```
proposals/       RFC documents. RFC-001 is the founding framework; RFC-002 onward
                 each fully specify one experiment from RFC-001 §8 before any code runs.
  INDEX.md       live status of every RFC

experiments/     one folder per experimental RFC, holding its code, data, and results
  RFC-00N-<slug>/
    README.md          scope, status, dependencies
    data/               corpus/dataset + sourcing notes (large files stay out of git)
    src/                pipeline code
    results/
      RESULTS.md        verdict against the RFC's Prediction, then discussion
      figures/
```

## The RFC lifecycle

1. **Draft** — write the RFC in `proposals/`. RFC-001 introduces the framework; each
   subsequent RFC fully specifies a single experiment from RFC-001 §8 — closing the gaps
   RFC-001 itself flags as open (effect sizes, null models, corpus-size requirements).
2. **Freeze** — once an experimental RFC is judged runnable, it's frozen. Further changes
   are appended to its version-history section, not made in place — the same convention
   RFC-001 already follows.
3. **Run** — code and data live in the matching `experiments/RFC-00N-.../` folder.
4. **Capture results** — findings go in that folder's `results/RESULTS.md`, opening with
   an explicit verdict (confirmed / refuted / mixed) against the RFC's Prediction.
5. **Feed back** — results get folded into RFC-001's placeholders, or motivate a new RFC,
   as a follow-up change.

## Current experiments

Seven experiments are queued from RFC-001 §8 (§§8.1–8.7). RFC numbers reflect the
program's recommended execution order — domain-literature maturity first, cross-domain
synthesis last — not §8's section order. See [`proposals/INDEX.md`](proposals/INDEX.md)
for the live status and the full sequencing rationale.

| RFC | § | Experiment |
|-----|---|------------|
| RFC-002 | 8.7 | The semantic layer as restored dampening (text-to-SQL) |
| RFC-003 | 8.4 | Enrichment-only noise amplification |
| RFC-004 | 8.6 | Structured memory over task horizon (agentic memory) |
| RFC-005 | 8.5 | The programming-language gradient |
| RFC-006 | 8.1 | Operationalizing ε, and coherence decay under fixed structure |
| RFC-007 | 8.3 | The scaling exponents δ and γ, and their trajectories |
| RFC-008 | 8.2 | Leverage growth and the phase boundary |

The motivation: rather than operationalizing $\epsilon$ in the abstract (the original
§8.1 framing), let domain experiments with strong prior art — SQL correctness, embedding
retrieval, agentic memory, code defects — each surface a working, domain-tested
inconsistency proxy first. RFC-006 then synthesizes those proxies instead of inventing
one cold, and RFC-007/RFC-008 build on RFC-006 in turn. RFC-002 is independent of this
chain and is already drafted; RFC-004 (the flagship) additionally requires a prior-art
survey before it can be frozen.

See also [`AGENTS.md`](AGENTS.md) for repo conventions, or [`CLAUDE.md`](CLAUDE.md) for
Claude-Code-specific guidance.
