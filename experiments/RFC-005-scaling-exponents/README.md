# RFC-005 — The Scaling Exponents δ and γ, and Their Trajectories

**Status:** Awaiting RFC. `proposals/RFC-005-scaling-exponents.md` has not been written yet.
**Source:** RFC-001 §8.3.
**Feeds:** RFC-004 (§8.2), which uses these exponents for its domain-specific boundary test.

## Scope

Measure the empirical growth order of both $\epsilon$ and $I$ in natural corpora across
domains with varying clustering strength, fitting $\epsilon_0(V) \sim V^{1+\delta}$ and
$I(V) \sim V^{\gamma}$ — and, critically, fitting them over successive growth windows
rather than once, to detect any trajectory $\delta(V)$, $\gamma(V)$ (per RFC-001 §3.4.1's
densification caveat). Also test whether community detection measurably lowers the
effective $\delta$ against the densification-driven tendency for it to rise.

## Layout

- `data/` — natural corpora across domains, with clustering-strength annotations.
- `src/` — exponent fitting per growth window; community-detection ablation.
- `results/` — `RESULTS.md` verdict plus `figures/`.

## Before running

Freeze `proposals/RFC-005-scaling-exponents.md` first — it needs to specify the domain
set, the growth-window construction, and the criterion for detecting a real trajectory
(vs. fitting noise) in $\delta(V)$/$\gamma(V)$.
