# PocketD Salvage Notes

Source:
https://github.com/matthewjameswatkins1978-cyber/PocketD

## Why not continue the old runtime

PocketD was valuable research and one of Matthew's earliest substantial programming projects. It proved hard things, but fuzzy musical judgement became increasingly coupled to rules and thresholds.

At the audited `main` state it contains roughly:

- 131 Python files;
- 47 test files;
- 22 `drummer/` modules;
- 28 demo scripts;
- a behaviour engine around 1,800 lines;
- extensive playtest, sanity, scoring, golden-reference, and diagnostic machinery.

The later `codex/live-lock-playtest` branch already recognised the problem. It preserved the large behaviour engine as research and added a simpler live vertical slice around "lose cleverness before losing time".

## Keep

1. Listen before playing.
2. Stability over nervous reactivity.
3. Uncertainty is real information.
4. Confidence is multidimensional.
5. Conservative entry.
6. Continue listening while playing.
7. Phrase memory.
8. Fast and slow adaptation.
9. Compact explainability.
10. Deterministic scenario testing.

## Change

### Rules for musical taste

Old:
encode BUILD, REDUCE, DROP, FILL, ANCHOR, etc. through interacting thresholds.

New:
derive objective evidence deterministically, then let a bounded reasoning layer choose high-level intent.

### Automated taste scoring

Old:
Musical Sanity, Arrangement Sanity, Musical Evaluation, Musical Doctor, golden references.

New:
automate safety and invariants; use human listening for taste.

A test should prove that a fill resolves on beat one. It should not pretend to prove the fill was a good artistic decision.

### Hard section switching

Old:
behaviour could jump when thresholds/states changed.

New:
beliefs are gradual; Hands morph future bars.

### Recovery

Old:
confidence collapse drove explicit behavioural states.

New:
recovery is normal musicianship. Keep the pocket, reduce commitment, listen, then rejoin.

## Code reuse policy

Do not import the old Python package into Nexus Bunny Deluxe.

Possible source material:
- groove examples;
- rhythmic feature ideas;
- phrase/repetition concepts;
- scenario definitions;
- timing invariants;
- live-lock lessons.

Anything reused must be re-expressed in the new typed architecture and justified independently.

## Historical win

PocketD answered a useful question:

**Which parts of "behave like a drummer" are mechanical enough to encode, and which parts become musical judgement?**

This project exists because we now have a better boundary between those two.
