# AGENTS.md

Conventions for any agent (human or AI) working in this repo. See `README.md` for the
high-level layout; this file covers the rules for extending it correctly.

## What this repo is

An RFC-driven research program testing the "Structure as Coherence Maintenance" framework
(RFC-001, "Resonance"). RFC-001 proposes seven experiments across its §8 (§§8.1–8.7);
each gets its own RFC in `proposals/` and its own execution folder in `experiments/`.

## RFC conventions

- **Naming:** `proposals/RFC-0NN-<kebab-slug>.md`, numbered by the program's recommended
  *execution* order — **not** RFC-001 §8's section order. RFC-002 targets §8.7, for
  instance, because it's a mature, ready-to-run domain experiment, not because §8.7 comes
  first; check `proposals/INDEX.md` for which RFC targets which §8.N and why it's ordered
  where it is, don't assume from the number. If the plan is re-sequenced, renumber the
  affected RFCs/experiment folders to keep this property true rather than letting numbers
  drift out of execution order — see `proposals/INDEX.md`'s numbering note.
- **Living framework, frozen protocols — both versioned.** RFC-001 (the framework) is a
  *living* document: refine it intentionally as evidence arrives, but record every change
  through the dated Version History and, if substantive, a bumped version label — never
  silent edits. Experiment RFCs (RFC-002 onward) are different: an experiment's protocol
  *freezes* once it goes to a run and must not change while it is Running, to protect
  pre-registration. Either way the fixed reference is the *version*, not the document —
  an experiment cites and is evaluated against the specific RFC-001 version it targets
  (e.g. RFC-002 → RFC-001 v8 §8.7), so refining RFC-001 later never invalidates a
  completed run. Refine RFC-001 in place when a change sharpens the same thesis; when a
  change is a genuinely new thesis rather than a refinement (e.g. the coherence-under-
  composition dynamics in §10), give it its own follow-up RFC that *extends* RFC-001
  rather than a revision that quietly diverges from it.
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
