# Nexus Bunny Deluxe

**A drummer that listens, joins, learns, and sometimes leads.**

Nexus Bunny Deluxe is a clean implementation of the Bunny Deluxe / Pocket Drummer idea for Audiotool Nexus.

The goal is not to generate drum tracks on command. The goal is to behave like a good drummer who cannot see the other musician and does not know the song, but can hear enough musical evidence to join the performance, keep it alive, learn its shape, and communicate through drumming.

## The thought experiment

Imagine a good drummer who is blind, in another room, and cannot talk to the guitarist.

They can still:

- listen for pulse and phrasing;
- enter cautiously with a useful simple beat;
- establish a shared "one";
- follow dynamics and space;
- notice repeated phrase shapes;
- make increasingly informed guesses;
- use fills as musical communication;
- lead toward a likely change;
- miss a change without wrecking the performance;
- recover smoothly and remember the mistake for next time.

That is Bunny.

## Why this version is different

The original PocketD repository proved several hard ideas, including pulse tracking, bar confidence, MIDI output, synthetic playtests, and stable live timing. It also became too complicated. Musical judgement was encoded as a growing forest of rules and thresholds, and local fixes repeatedly created new musical problems.

This version separates three jobs:

```
Audiotool project
      |
      v
   OBSERVER
musical facts and recent history
      |
      v
    BRAIN
fuzzy musical judgement
      |
      v
    HANDS
safe deterministic drum performance
      |
      v
Audiotool drum track
```

The **Brain** may use an AI model for ambiguous musical judgement.

The **Hands** do not. Timing, note placement, density limits, velocities, fills, continuity, track ownership, and other performance invariants remain deterministic and testable.

The model never gets permission to spray arbitrary MIDI into the project.

## Performance contract

Bunny behaves as if there is an audience.

1. Keep the performance alive.
2. Preserve pulse and continuity before trying to be clever.
3. When uncertain, simplify and listen.
4. Do not correct mistakes by snapping abruptly to a new behaviour.
5. Recover by playing through the mistake.
6. Lead only when confidence has earned the risk.
7. Stopping is a musical decision, not an error response.
8. Bunny writes only to Bunny-owned project entities.
9. Every AI decision must degrade to a safe deterministic fallback.

> **When uncertain, preserve continuity. When confident, earn the right to take initiative.**

## The musical conversation

```
Human plays
  -> Bunny observes
  -> Bunny forms a belief
  -> Bunny answers musically
  -> Human reacts
  -> Bunny learns from the reaction
```

A fill is therefore not just decoration. It can mean:

- "I have found the bar. We are together now." (handshake)
- "I think a change belongs here." (predictive cue)
- "I heard that. Here is my answer." (response)

The important test is not whether Bunny labels a chorus correctly. It is whether Bunny can occasionally play something that causes the other musician to respond as if another musician were in the room.

## Audiotool hackathon slice

Audiotool Nexus is the first laboratory because it exposes the project document directly. Bunny can inspect timeline notes, positions, velocities, project tempo and time signature, observe project changes, and write its own drum material back into the same multiplayer project.

For the hackathon, we do **not** attempt to solve raw live guitar audio at the same time.

The first vertical slice is:

1. Connect to an Audiotool project.
2. Let the user nominate one or more source tracks.
3. Observe a bounded musical window.
4. Derive density, accents, repetition, space, energy, phrase evidence, and recent changes.
5. Join with a restrained pocket.
6. Place a handshake fill when Bunny has established a useful shared phrase boundary.
7. Continue observing while playing.
8. Adapt future bars gradually when the source changes.
9. Make one bounded predictive cue when evidence for a transition is strong enough.
10. If the prediction is wrong, preserve the groove, recover gradually, and update session memory.
11. Write only to a Bunny-owned drum track/device.

## Fast and slow learning

### Fast: session understanding

- likely phrase length;
- recurring rhythmic fingerprints;
- change points;
- energy trends;
- where transitions have happened in this session;
- which predictions were followed or contradicted.

### Slow: player preference

- preferred density;
- tolerance for fills;
- cymbal restraint;
- how strongly Bunny should lead;
- which Bunny edits the player keeps, deletes, simplifies, or moves.

This is lightweight memory and evidence, not model training.

## NOD

The original one-button idea stays.

**NOD** means:

> **Pay attention. Something musically important is happening around here.**

It does not mean "chorus". The Brain interprets it in context. A future version can map NOD to a MIDI footswitch.

## Technology direction

- TypeScript, because the Audiotool Nexus JS/TS SDK has the richest real-time integration.
- Vite for the browser companion app.
- Exact pinned Nexus SDK version behind a narrow adapter because Nexus is early alpha.
- Pure TypeScript music analysis and rendering core.
- Pluggable AI reasoner with structured output.
- Offline Nexus documents for deterministic integration tests.
- No Rust/WASM in the hackathon MVP unless measurement proves it is needed.

## PocketD policy

Reuse **ideas and evidence**, not the old runtime architecture.

Keep:

- listen first, play second;
- stability over nervous reactivity;
- uncertainty as a first-class concept;
- separate kinds of confidence;
- stable timing;
- simple entry;
- graceful degradation and recovery;
- phrase memory;
- fast and slow adaptation;
- decision traces;
- synthetic scenario testing;
- the later "lose cleverness before losing time" insight.

Retire from the new core:

- the giant threshold-driven behaviour engine;
- broad state-machine choreography for musical taste;
- automated Musical Doctor taste scoring;
- golden-reference taste bureaucracy;
- raw-audio onset/pulse tracking as a hackathon requirement;
- hundreds of interacting rules for fuzzy judgement;
- arbitrary AI MIDI generation.

Original research repository:
https://github.com/matthewjameswatkins1978-cyber/PocketD

## Success criterion

> **Bunny makes a musical cue, and the player responds to it naturally.**

That is the beginning of a bandmate.
