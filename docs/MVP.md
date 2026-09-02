# Hackathon MVP

## Objective

Prove one thing convincingly:

> **Bunny can observe changing musical material inside Audiotool, join conservatively, communicate a musical belief, survive being wrong, and adapt without breaking the performance.**

## Demo story

### 1. Bunny listens

The project contains a simple 8-bar source phrase on a nominated note track.

Bunny connects and initially writes nothing.

The diagnostic view shows repeated phrase evidence growing.

### 2. Bunny joins

Bunny creates its own drum kit and timeline and writes a simple useful pocket.

At the end of the established phrase it uses a small **handshake fill**:

"I have found our bar and phrase. We are together."

### 3. Musical body language

The user makes the next passage more assertive through velocity, density, phrase ending, or a combination.

Bunny does not instantly switch patterns.

It develops gradually:
- slightly stronger backbeat;
- modest hat development;
- carefully bounded kick interaction.

### 4. Bunny leads and gets it wrong

Evidence suggests a change after the next phrase.

Bunny places a restrained predictive fill.

The user deliberately does **not** change.

Bunny:
- does not crash into a new full pattern;
- keeps time;
- reduces the attempted change;
- settles back into the pocket;
- records that the transition did not occur.

"Wrong" does not mean "broken".

### 5. Bunny learns and leads

Later, stronger/repeated evidence appears.

Bunny cues again.

This time the human makes the change.

Bunny moves smoothly with it.

The two sides have influenced one another.

## Must have

- Nexus OAuth/project connection.
- Exact pinned SDK.
- Source-track selection.
- Tempo/signature reading.
- Note/region observation.
- Deterministic feature extraction.
- Phrase repetition/change evidence.
- Bunny-owned drum device and track.
- Simple pocket renderer.
- Safe dynamics.
- Handshake fill.
- Structured Brain interface.
- Safe fallback on Brain failure.
- One predictive cue.
- Gradual recovery from a wrong prediction.
- Bounded session memory.
- Decision trace.
- Offline Nexus integration tests.
- One rehearsed demo project.

## Should have

- NOD button.
- Detect human edits to Bunny output as preference evidence.
- Small inspectable player profile.
- One alternative kit/pocket.

## Explicitly not MVP

- raw microphone guitar listening;
- live onset detection;
- pitch/chord transcription;
- genre recognition;
- dozens of grooves;
- advanced fill generation;
- odd meter;
- cloud profile service;
- full drummer personas;
- reinforcement learning;
- model-generated MIDI;
- elaborate GUI;
- resurrection of PocketD's behaviour engine.

## Acceptance criteria

### Safety

- Bunny modifies only Bunny-owned entities.
- Reprocessing a source revision does not duplicate notes.
- Model failure produces a stable pocket.
- Generated hits stay inside velocity/density limits.
- Human material is never rewritten.

### Continuity

- Bunny joins only after a useful observation window.
- First entry is simple.
- Handshake fill resolves to stable beat one.
- Intensity changes produce bounded gradual changes.
- Wrong predictive cue does not cause an abrupt whole-pattern jump.
- Recovery occurs over future bars while pocket continues.
- Structural uncertainty alone never stops Bunny.

### Interaction

- Bunny makes at least one cue before a likely transition.
- Memory distinguishes followed vs contradicted cues.
- A repeated similar situation can alter the next decision.
- Demo shows human -> Bunny -> human influence.

### Engineering

- Observer, Session Model, Brain schema, Hands, Nexus adapter are separate.
- Core music logic works without live Audiotool.
- Offline integration tests cover ownership/idempotence.
- Brain output is schema validated and clamped.
- Trace records observation, beliefs, intent, rendered revision.

## Reliability mode

Brain decisions happen ahead of future bars, not at the last millisecond.

Provide:

1. **Live reasoner** for the actual AI behaviour.
2. **Replay/stub reasoner** for the exact demo fixture if an external model provider is unavailable.

The replay mode is insurance, not the central demo.

## What success looks like

A judge should understand it by listening:

1. Bunny listens.
2. Bunny joins carefully.
3. Bunny notices the musician.
4. Bunny says something musically.
5. The musician answers.
6. Bunny changes because of that answer.
