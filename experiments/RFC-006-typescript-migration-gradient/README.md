# RFC-006 — The Programming-Language Gradient

**Status:** Awaiting RFC. `proposals/RFC-006-typescript-migration-gradient.md` has not been written yet.
**Source:** RFC-001 §8.5.

## Scope

Test whether the volume threshold at which coherence problems become intolerable is
higher for stronger type disciplines, exploiting JS-to-TS migrations as a natural
experiment (same codebase/team on both sides of the type-discipline boundary). Mine
GitHub-derived corpora for such pairs; use LoC as the proxy for $V$ and defect density
normalized by LoC (pre- vs. post-migration) as the proxy for coherence failure.

RFC-001 flags this as the program's hardest empirical lift — type discipline is
confounded with team size, project maturity, and code quality, none of which can be
randomized. Within-project migration comparisons should be preferred over cross-project
ones wherever the data permits.

## Layout

- `data/` — mined repositories, migration identification, LoC/defect-density extraction.
- `src/` — pre/post-migration windowing, threshold estimation, confound-sensitivity checks.
- `results/` — `RESULTS.md` verdict plus `figures/`.

## Before running

Freeze `proposals/RFC-006-typescript-migration-gradient.md` first — it needs to specify
the corpus-mining criteria for a valid migration, the defect-density proxy precisely
(what counts as a defect), and how team-size/project-age sensitivity will be reported.
