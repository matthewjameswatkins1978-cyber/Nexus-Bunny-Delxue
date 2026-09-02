# Architecture

## Goal

Allow fuzzy musical judgement without giving an AI model control over timing safety or arbitrary project mutation.

```
                    +-------------------+
Audiotool Nexus --->|   Nexus Adapter   |
                    +---------+---------+
                              |
                              v
                    +-------------------+
                    |     Observer      |
                    | deterministic     |
                    +---------+---------+
                              |
                      MusicalObservation
                              |
                              v
                    +-------------------+
                    |   Session Model   |
                    | history + beliefs |
                    +---------+---------+
                              |
                         BrainContext
                              |
                              v
                    +-------------------+
                    |      Brain        |
                    | fuzzy judgement   |
                    +---------+---------+
                              |
                         DrummerIntent
                              |
                              v
                    +-------------------+
                    |      Hands        |
                    | deterministic     |
                    +---------+---------+
                              |
                         DrumPlan
                              |
                              v
                    +-------------------+
                    |  Nexus Writer     |
                    | Bunny-owned only  |
                    +-------------------+
```

## Nexus Adapter

Responsibilities:

- authenticate and attach to a project;
- pin and isolate the SDK version;
- subscribe to relevant entity changes;
- query source tracks and Bunny-owned tracks;
- expose tempo and time signature;
- translate Nexus entities into stable internal types;
- execute writer transactions.

The rest of Bunny must not import Nexus entity types.

Nexus is early alpha. One adapter should absorb SDK churn.

## Observer

Pure deterministic code.

Input:
- selected source notes/regions;
- tempo and signature;
- bounded recent timeline;
- previous observation.

Output:

```ts
type MusicalObservation = {
  window: { startBar: number; endBar: number }
  tempoBpm: number
  signature: { numerator: number; denominator: number }

  onsetDensity: number
  velocityMean: number
  velocityTrend: number
  spaceRatio: number

  beatAccentVector: readonly number[]
  subdivisionHistogram: readonly number[]
  phraseFingerprint: string
  repetitionStrength: number
  changeScore: number

  candidatePhraseLengths: readonly {
    bars: number
    confidence: number
  }[]

  sourceRevision: string
}
```

Do not put interpretation such as "chorus" here.

## Session Model

Maintains bounded conversation history.

Responsibilities:

- repeated phrase fingerprints;
- likely transition positions;
- previous Brain predictions;
- what happened after Bunny cues;
- separate confidence dimensions;
- musical risk budget;
- fast session memory;
- slow player preferences.

Example beliefs:

```ts
type MusicalBeliefs = {
  timeConfidence: number
  phraseConfidence: number
  changeLikelihood: number
  changeBarsAhead: number | null
  energyDirection: "down" | "flat" | "up"
  uncertainty: number
  riskBudget: number
}
```

These are beliefs, not rigid state-machine modes.

## Brain

The fuzzy component.

Input:
- current observation;
- beliefs;
- recent phrase summaries;
- current Bunny performance;
- recent human response to Bunny;
- optional NOD;
- bounded player preferences.

Output is structured `DrummerIntent`, never MIDI.

```ts
type DrummerIntent = {
  continuity: "hold" | "morph" | "simplify"
  targetEnergy: number
  targetDensity: number
  leadAmount: number
  cymbalAmount: number
  kickRelationship: number

  cue:
    | { kind: "none" }
    | {
        kind: "handshake" | "predictive"
        targetBar: number
        sizeBeats: 1 | 2 | 4
        strength: number
      }

  confidence: number
  reason: string
}
```

Keep the schema small.

If the Brain fails, fall back to:
- hold;
- modest energy;
- no cue;
- no new complexity.

The Brain is not queried at audio rate. Reason at phrase-safe boundaries or after meaningful project changes.

## Hands

Pure deterministic rendering.

Responsibilities:

- choose or morph a safe base pocket;
- render kick/snare/hat events;
- enforce velocity ranges;
- enforce density ceilings;
- construct bounded fills;
- resolve cues cleanly into beat one;
- avoid pathological simultaneous hits;
- preserve continuity across revisions;
- render gradual recovery;
- seed variation deterministically.

This is where "do not hit things too hard" lives.

A model can request "stronger". It cannot set every note to maximum velocity.

## Nexus Writer

Only component allowed to mutate the Audiotool project.

Rules:

- create dedicated Bunny drum entities;
- retain ownership identifiers;
- never modify user-owned source notes;
- re-query while holding the transaction lock;
- apply only managed Bunny regions;
- use revisions so stale plans cannot overwrite newer work;
- support clean reset/removal.

Nexus exposes note position, duration, MIDI pitch and velocity, note tracks/regions/collections, project config, and GM drum presets. This is enough for a typed Bunny drum timeline.

## Two timescales

Fast:
```
observe -> update beliefs -> maybe reason -> render future bars
```

Slow:
```
human keeps/deletes/moves/simplifies Bunny output
-> bounded preference update
-> inspectable player profile
```

## Recovery

When Bunny is contradicted:

1. Do not rewrite the current beat violently.
2. Preserve the pocket.
3. Reduce optional layers.
4. Morph future bars toward the new situation.
5. Restore variation only after confidence returns.
6. Store what preceded the missed change.

Recovery belongs in deterministic policy, not in model improvisation.

## Testing

### Unit

Test Observer, Session Model, Hands.

Test invariants, not taste:
- density bounds;
- velocity bounds;
- stable fingerprints;
- deterministic rendering;
- fills resolve correctly;
- uncertainty reduces optional behaviour;
- player tracks are untouched.

### Brain contract

- structured output validation;
- malformed output rejected;
- timeout/error fallback;
- extreme values clamped.

### Nexus integration

Use `createOfflineDocument()`:
- source notes observed;
- Bunny track created;
- bounded updates;
- user entities untouched;
- repeated processing is idempotent.

### Musical scenarios

Keep a small suite:
- repeated 8-bar riff;
- gradual build;
- unexpected extra verse after a predictive cue;
- successful predicted change;
- sudden simplification;
- ending / empty tail.

Automated tests prove safety and consistency. Human listening proves musicianship.

## Suggested tree

```
src/
  nexus/
    adapter.ts
    reader.ts
    writer.ts
    ownership.ts

  music/
    observation.ts
    observe.ts
    fingerprint.ts
    phrase.ts

  session/
    model.ts
    beliefs.ts
    memory.ts
    preferences.ts

  brain/
    schema.ts
    reasoner.ts
    fallback.ts

  performance/
    hands.ts
    pocket.ts
    fills.ts
    morph.ts
    dynamics.ts

  app/
    controller.ts

  ui/
    ...

tests/
  fixtures/
  scenarios/
```

Keep core music logic usable without Audiotool.
