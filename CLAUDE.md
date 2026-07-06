# CLAUDE.md

Session-specific guidance for Claude Code in this repo. Repo-wide conventions (naming,
folder layout, RFC lifecycle, writing style) live in [`AGENTS.md`](AGENTS.md) — read that
first; this file only adds what's specific to working here as Claude.

## What this repo is

An RFC-driven research program testing the "Structure as Coherence Maintenance" framework
(RFC-001). Seven experiments are queued in `proposals/INDEX.md`, each destined for its own
RFC in `proposals/` and its own folder in `experiments/`. RFC numbers reflect the
program's recommended *execution* order (domain-literature maturity first, cross-domain
synthesis last), not RFC-001 §8's section order — RFC-002 targets §8.7, not §8.1 — so
check `proposals/INDEX.md` for the current RFC-to-§8.N mapping and sequencing rationale
before assuming one.

## When asked to draft an experimental RFC

- Assign the next free RFC number regardless of which §8.N it targets.
- Start from the corresponding §8.N section of `proposals/RFC-001-resonance-structure-coherence.md`
  — its Prediction and Method are the seed, not something to rederive from scratch.
- Explicitly close the gaps RFC-001 names as open for that experiment (see `AGENTS.md`).
- Follow RFC-001's version-history and "Status of this document" conventions rather than
  inventing a new format.
- Update `proposals/INDEX.md` in the same change.

## When asked to run an experiment

- Confirm the matching RFC is frozen first (check `proposals/INDEX.md`) — don't run
  against a still-drafting RFC.
- Work inside `experiments/RFC-0NN-.../`; keep large data out of git per `AGENTS.md`.
- Write findings to `results/RESULTS.md` as an explicit verdict against the RFC's
  Prediction, before any narrative discussion.

## Literature and prior-art tasks

Sections like §8.6.1 (prior-art for the agentic-memory experiment) call for positioning
against existing work before a run. These are exactly the kind of broad, multi-source
lookups worth delegating — use the Agent tool (an Explore or general-purpose research
agent) rather than asserting prior-art familiarity from memory.

## Git

This repo's branch/push conventions are set by the session's operating instructions, not
by this file — follow whatever branch is designated for the current session.
