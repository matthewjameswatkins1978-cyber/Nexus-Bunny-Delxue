# Architectural Decisions

## ADR-001: Clean repository

**Accepted.** PocketD remains a research archive. Nexus Bunny Deluxe has no old runtime dependency.

## ADR-002: TypeScript first

**Accepted.** Audiotool's JS/TS SDK has the richest real-time project integration. Do not add a cross-language boundary without evidence it helps.

Rust/WASM remains an option later for measured performance-sensitive work such as live audio perception.

## ADR-003: Nexus behind an adapter

**Accepted.** Core music modules do not import Nexus entity types.

Reason: Nexus is early alpha and explicitly warns of breaking changes.

## ADR-004: AI chooses intent, never raw MIDI

**Accepted.** A model may decide fuzzy high-level musical intent using a small structured schema. It may not directly write notes.

Judgement is fuzzy; timing safety and performance constraints are not.

## ADR-005: Continuity outranks correctness

**Accepted.** Bunny behaves as if an audience is listening. A wrong structural belief is handled musically.

## ADR-006: Recovery is deterministic policy

**Accepted.** If evidence contradicts Bunny, optional layers reduce and future bars morph toward the new situation.

Do not depend on a model inventing a tasteful recovery each time.

## ADR-007: No raw audio requirement in MVP

**Accepted.** Use Audiotool project state, especially note/region data, as the first observation source.

This isolates fuzzy musicianship from the separate hard problem of live raw-audio perception.

## ADR-008: Fills are communication

**Accepted.** MVP distinguishes handshake and predictive fills.

## ADR-009: NOD is deliberately ambiguous

**Accepted.** NOD means "pay attention around here", not "go to chorus".

## ADR-010: Tests prove invariants, humans judge taste

**Accepted.** Do not rebuild an automated musical taste bureaucracy.

Tests cover correctness, safety, continuity constraints, ownership, idempotence, and structured contracts. Listening/playtesting judges whether Bunny actually feels musical.
