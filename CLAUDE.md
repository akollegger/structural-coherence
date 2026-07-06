# CLAUDE.md

Session-specific guidance for Claude Code in this repo. Repo-wide conventions (naming,
folder layout, RFC lifecycle, writing style) live in [`AGENTS.md`](AGENTS.md) — read that
first; this file only adds what's specific to working here as Claude.

## What this repo is

An RFC-driven research program testing the "Structure as Coherence Maintenance" framework
(RFC-001). Six experiments are queued in `proposals/INDEX.md`, each destined for its own
RFC in `proposals/` and its own folder in `experiments/`.

## When asked to draft an experimental RFC (RFC-002..007)

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

Sections like RFC-007's §8.6.1 call for positioning against existing work before a run.
These are exactly the kind of broad, multi-source lookups worth delegating — use the
Agent tool (an Explore or general-purpose research agent) rather than asserting prior-art
familiarity from memory.

## Git

This repo's branch/push conventions are set by the session's operating instructions, not
by this file — follow whatever branch is designated for the current session.
