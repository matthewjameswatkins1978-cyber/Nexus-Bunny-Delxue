# Product Constitution

## Product sentence

**Bunny Deluxe is a behavioural drummer that reads musical intent from behaviour and answers with behaviour.**

It is not a prompt-to-drums generator.

## Reference musician

The reference is a competent drummer who:

- cannot see the other player;
- does not know the song;
- cannot talk to the other player;
- can hear enough of the performance to form beliefs;
- must keep playing as if an audience is present.

Bunny should be judged against how that drummer behaves, including how they make and recover from mistakes.

## Priority order

1. **Continuity**: keep the performance coherent.
2. **Time**: maintain a trustworthy shared rhythmic frame.
3. **Appropriateness**: match broad intensity, space, and density.
4. **Understanding**: build and revise beliefs about phrases and changes.
5. **Communication**: make readable musical gestures.
6. **Initiative**: lead only when evidence supports it.
7. **Novelty**: be interesting only after the previous six are safe.

Any feature that improves a lower item by damaging a higher item is suspect.

## The rule for mistakes

**Bunny is allowed to be wrong. Bunny is not allowed to be wrong violently.**

A missed section is normal musicianship.

Example:

- Bunny expects another verse.
- The player enters a chorus.
- Bunny does not instantly replace the beat.
- Bunny preserves the pocket.
- Bunny reduces commitment briefly.
- Bunny introduces chorus-like characteristics over the next bar or two.
- Bunny settles into the new situation.
- Bunny records the evidence that preceded the missed change.

The listener hears a recovery, not a software correction.

## Beliefs, not hard labels

Avoid requiring hard labels such as VERSE or CHORUS.

Useful beliefs are closer to:

- repetition is strong;
- the phrase probably resolves in two bars;
- energy is rising;
- the player is leaving more space;
- this gesture preceded a change twice before;
- a transition is likely soon;
- I am not confident enough to lead.

Time confidence is not structure confidence.

## Musical risk budget

Low confidence:
- maintain or simplify;
- avoid fills;
- make space;
- listen.

Medium confidence:
- support;
- make small dynamic adjustments;
- use restrained variation.

High confidence:
- make a readable cue;
- anticipate a change;
- take a little initiative.

Risk is earned by evidence and lost quickly when contradicted.

## Fills as language

### Handshake fill

"I have found our phrase and our one."

Used when Bunny has listened long enough to join properly.

### Predictive fill

"I think we should change here."

Occurs before the expected transition and therefore risks being wrong.

### Response fill

"I heard your gesture."

The MVP needs handshake plus one bounded predictive cue. Response fills can follow later.

## Musical body language

Infer intent from trends and combinations, never one isolated feature.

Useful evidence includes:

- attack density;
- velocity / intensity trend;
- rhythmic insistence;
- simplification;
- silence and space;
- repeated phrase endings;
- syncopation changes;
- phrase-level repetition;
- new or removed notes;
- player edits to Bunny output;
- NOD timing.

"Played louder" is evidence, not a direct command.

## NOD

NOD means:

**"Pay attention. Something important is happening around here."**

It is intentionally underspecified. It may strengthen evidence for a transition, ending, build, or other contextual interpretation.

Future physical input:
- MIDI footswitch;
- keyboard shortcut;
- hardware button.

## Learning

### Session memory

Fast changing:
- phrase fingerprints;
- likely phrase lengths;
- observed transitions;
- recent predictions;
- whether cues were followed or contradicted;
- temporary interaction tendencies.

### Player profile

Slow changing:
- preferred activity;
- fill tolerance;
- cymbal restraint;
- leading tendency;
- response to dynamics.

The profile must be inspectable and resettable.

## UI philosophy

The actual musical interface is the music.

Development diagnostics may show observations, beliefs, risk, last Brain decision, and what Bunny learned. The finished player should not need to stare at confidence meters.

## North-star test

> **Does this make it more likely that the player reacts to Bunny as another musician rather than as software?**
