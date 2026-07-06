# AGENTS.md

Conventions for any agent (human or AI) working in this repo. See `README.md` for the
high-level layout; this file covers the rules for extending it correctly.

## What this repo is

An RFC-driven research program testing the "Structure as Coherence Maintenance" framework
(RFC-001, "Resonance"). RFC-001 proposes seven experiments across its §8 (§§8.1–8.7);
each gets its own RFC in `proposals/` and its own execution folder in `experiments/`.

## RFC conventions

- **Naming:** `proposals/RFC-0NN-<kebab-slug>.md`, numbered in the order RFCs are
  written — **not** in RFC-001 §8's section order. RFC-002 targets §8.7, for instance,
  because it was written first; check `proposals/INDEX.md` for which RFC targets which
  §8.N, don't assume from the number.
- **Frozen means frozen.** RFC-001 states its own frozen status explicitly ("Status of
  this document" section) and records changes via a dated Version History list rather
  than silent edits. Follow that convention for every RFC: once an RFC is frozen, don't
  edit its body — append a version-history entry and, if the change is substantive, bump
  the version label. Note that RFC-001 itself distinguishes a frozen *argument*
  (Sections 1–7, 9–11) from an extensible §8 — new experimental sections (like §8.7) can
  be appended to §8 without unfreezing the rest, provided the version history says so.
- **An experimental RFC must close the gaps RFC-001 leaves open** for that experiment
  before it can be frozen: effect sizes, the model-comparison/null-model criterion,
  corpus-size or power requirements, and (for whichever RFC targets §8.6) the §8.6.1
  prior-art survey.
- **Update `proposals/INDEX.md` in the same change** whenever an RFC's status changes or
  a new RFC is added, including the §8.N it targets.

## Experiment folder conventions

- One folder per experimental RFC: `experiments/RFC-0NN-<slug>/`, slug matching the RFC
  filename.
- Standard subfolders: `data/`, `src/`, `results/` (containing `RESULTS.md` and
  `figures/`).
- `data/README.md` documents sources, construction method, and licensing. Don't commit
  raw data above a few MB — `.gitignore` it and record the external location (bucket,
  DVC remote, etc.) in that same README.
- **Do not start building an experiment's `data/`/`src/` until its RFC is frozen.** A
  still-drafting RFC means open questions about method, not something to improvise
  around in code.
- `results/RESULTS.md` opens with an explicit **Verdict** (confirmed / refuted / mixed)
  stated against the RFC's Prediction, before any narrative discussion. Quote or restate
  the Prediction for reference immediately after.

## Writing style

RFC and RESULTS prose follows RFC-001's register: precise, hedged where the argument is
genuinely uncertain, plain where it isn't. Don't inflate confidence in a results write-up
beyond what the data shows, and don't hedge past what the data actually settles.

## Research tasks

Literature-survey requirements (e.g. the §8.6.1 prior-art check for whichever RFC targets
§8.6) should be treated as real blocking work, not a formality — confirm the framing
isn't already occupied before freezing the RFC that depends on it.
