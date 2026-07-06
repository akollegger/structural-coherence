# RFC-008 — Leverage Growth and the Phase Boundary

**Status:** Awaiting RFC. `proposals/RFC-008-leverage-phase-boundary.md` has not been written yet.
**Source:** RFC-001 §8.2.
**Depends on:** RFC-007 (§8.3) for domain-specific $\delta$, $\gamma$ estimates — see note below.

## Scope

Grow matched corpora under different structural-growth policies (fixed, sublinear, linear,
matched-to-$\beta$) and test whether the boundary predicted in RFC-001 §3.4 separates
coherence-maintaining trajectories from degrading ones — specifically, whether the *sign*
of $\beta = 1+\delta-\gamma$ sorts them, not just the magnitude of $\delta$.

## Dependency note

This experiment can run with the worst-case $\beta = 1$ on its own, but the sharper test —
whether the domain-specific composite exponent predicts the boundary better than the
worst case — needs $\delta$ and $\gamma$ estimates from RFC-007. Sequence accordingly, or
run both with the worst-case bound first and revisit once RFC-007 has results. This is
the last experiment in the program's recommended order — it depends transitively on
RFC-006 (epsilon) through RFC-007.

## Layout

- `data/` — matched corpora under each growth policy, and construction notes.
- `src/` — leverage estimation ($\phi$, $\sigma$ measurement) and boundary comparison.
- `results/` — `RESULTS.md` verdict plus `figures/`.

## Before running

Freeze `proposals/RFC-008-leverage-phase-boundary.md` first — it needs to specify the
growth policies precisely, how $\Lambda$ is measured empirically, and the criterion for
"separates maintaining from degrading" (an effect size, not just a visual boundary).
