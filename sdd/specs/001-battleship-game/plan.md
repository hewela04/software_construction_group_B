# Implementation Plan: Browser Battleship Game

**Branch**: `001-battleship-game` | **Date**: 2026-10-22 | **Spec**: [spec.md](./spec.md)

**Input**: Requirements and user scenarios in this feature's [specification](./spec.md), governed by the [SDD constitution](../../.specify/memory/constitution.md).

## Summary

Implement the specified human-versus-computer Battleship game as a new,
independent browser application at `sdd/battleship.html`. The implementation
must be derived only from the SDD constitution and feature specification. It
must not copy, import, adapt, or otherwise depend on the root-level
`battleship.html`. Deliver the placement, play, result, and restart journeys
described in the specification without a backend, database, or login.

## Technical Context

**Language/Version**: Browser-native HTML, CSS, and JavaScript; use features
supported by current desktop and mobile browsers.

**Primary Dependencies**: None planned. The deliverable is a standalone
`sdd/battleship.html` file and must not import code or assets from outside the
SDD project folder.

**Storage**: In-memory match state; the constitution and specification require
no backend, database, login, or persistent game data.

**Testing**: Verify behavior against the acceptance scenarios and rule checks in
[quickstart.md](./quickstart.md), using browser-based manual checks or
automated tests if an appropriate SDD-local test harness is established.
Validation must exercise the SDD implementation, not the root-level game.

**Target Platform**: Current desktop and mobile browsers

**Project Type**: Independent static, client-side browser game

**Performance Goals**: Responsive interaction for two 10-by-10 boards and the
specified five-ship fleets; no server-side processing is required.

**Constraints**: Keep the game browser-only; implement into a new file within
`sdd/`; do not modify, copy, import, or reuse code from the root
`battleship.html`; follow the specification for all game behavior and required
terminal messages.

**Scale/Scope**: One human player, one computer opponent, two 100-cell boards,
five ships per fleet, and one local match at a time.

## Constitution Check

| Gate | Result | Evidence |
|---|---|---|
| Simple, maintainable code | PASS | A standalone browser game is appropriate to this small feature; avoid unjustified abstractions and dependencies. |
| Specification fidelity | PASS | The SDD feature specification defines the user journeys, game rules, interface expectations, and success criteria. |
| Verified game rules | PASS | The quickstart specifies checks for placement validity, hits/misses, win/loss, and restart. |
| Browser-first scope | PASS | The game runs in a browser without a backend, database, or login. |
| Reviewable changes | PASS | The implementation target is isolated to a new SDD-local game file and SDD-local validation. |
| Independent implementation | PASS | The SDD implementation must be created from the constitution and specification, with no code reuse or dependency on the root game. |

No constitution violations or unresolved specification clarifications are
identified for planning.

## Design Outline

- Create a new standalone game file at `sdd/battleship.html`; it is the
  implementation target, not a copy or derivative of another game file.
- Translate the SDD requirements into game state and interaction behavior:
  fleet setup, placement preview and validation, randomized fleets, turn
  resolution, shot feedback, sunk-ship reporting, terminal results, and restart.
- Validate manual and randomized placements against the specification:
  straight, in bounds, exact required ship lengths, and non-overlapping while
  permitting ships to touch.
- Keep the computer's unhit ships hidden from the player. Use the exact
  terminal messages required by the spec: “Congrats, you won!” and “Game over!
  Computer wins.”
- Present the required coordinate labels and board layout, and support the
  specified responsive behavior and keyboard access.
- Validate the new SDD-local implementation with the journeys in
  [quickstart.md](./quickstart.md). Do not use the root game as a test fixture,
  implementation reference, or runtime dependency.

## Project Structure

### Documentation (this feature)

```text
sdd/
├── battleship.html                 # New independent game implementation
├── .specify/
│   └── memory/constitution.md
└── specs/001-battleship-game/
    ├── spec.md
    ├── plan.md
    ├── research.md
    ├── data-model.md
    ├── quickstart.md
    ├── checklists/requirements.md
    └── tasks.md                    # Created by the later /speckit-tasks workflow
```

No external API contract is specified: the game is browser-only and has no
programmatic service interface.

**Structure Decision**: Create and validate a separate standalone
`sdd/battleship.html`. Keep the specification, constitution, plan, and
validation guide as the source of truth. The root-level game is outside the
implementation boundary.

## Complexity Tracking

No constitution violations require justification.

## Post-Design Constitution Check

PASS. The implementation boundary is isolated to a new SDD-local file, the
behavior is grounded in the SDD constitution and specification, and the plan
requires independent verification against the specification.
