# Research: Browser Battleship Game

## Research Scope

This plan is grounded in the SDD feature specification and
[constitution](../../.specify/memory/constitution.md). No implementation
inspection is part of this research. In particular, the root-level
`battleship.html` is not a design source, code source, dependency, test fixture,
or behavior authority for the SDD implementation.

## Decisions

### Create a separate SDD-local browser game

- **Decision**: The future implementation target is a new
  `sdd/battleship.html` file.
- **Rationale**: The user requires an SDD-local game file, and the constitution
  requires browser-first delivery while favoring simple, maintainable code.
  Keeping the deliverable standalone makes the implementation boundary clear.
- **Alternatives considered**: Modifying or embedding another game file.
  Rejected because it would violate the explicit independence requirement.

### Derive behavior only from the SDD requirements

- **Decision**: Treat the SDD specification as the source of detailed game
  behavior and the SDD constitution as the governing implementation and
  verification principles.
- **Rationale**: The specification defines user journeys, fleet composition,
  placement rules, turn behavior, feedback, terminal outcomes, restart, and
  measurable success criteria. The constitution requires fidelity to those
  requirements and verification of essential rules.
- **Alternatives considered**: Adopting interface, visual, or behavioral
  choices from an existing implementation. Rejected; those choices are outside
  the SDD requirements and could improperly constrain the independent design.

### Use browser-native delivery without a backend

- **Decision**: Build a browser game requiring no backend, database, or login.
- **Rationale**: This is an explicit technical constraint in the constitution
  and functional requirement FR-001.
- **Alternatives considered**: Server-hosted game logic or persistent match
  storage. Neither is needed by the specified user journeys.

### Verify the SDD implementation against acceptance criteria

- **Decision**: Validate the new file directly using the repeatable checks in
  [quickstart.md](./quickstart.md), adding automated tests if a suitable
  SDD-local harness is selected during implementation.
- **Rationale**: The constitution allows automated tests or manual checks,
  depending on practicality, and explicitly identifies placement, hit/miss,
  win/loss, and restart verification.
- **Alternatives considered**: Testing by opening or exercising the root game.
  Rejected because that would not validate the independent SDD implementation.

## Requirement-Derived Constraints

- Board size and labels: two 10-by-10 boards, columns A-J and rows 1-10
  (FR-002).
- Fleet: exactly five straight ships per side with lengths 4, 3, 3, 2, and 2
  (FR-004).
- Placement: horizontal or vertical, entirely in bounds, no overlap; touching
  is permitted (FR-005 through FR-009).
- Play: alternating player/computer turns, unique targets, hit/miss feedback,
  sunk-ship reporting, concealed unhit computer ships, and specified end
  conditions (FR-011 through FR-021).
- Reset: clear results, return to manual player setup, and generate a new
  computer fleet (FR-022 and FR-023).
- Presentation: required board identifiers and responsive layout (FR-003 and
  FR-024).

## Planning Consequences

- Implement only in the new `sdd/battleship.html` file unless implementation
  work later demonstrates that an additional SDD-local file is necessary.
- Keep the SDD spec and constitution authoritative; do not copy or depend on
  root-level application code, styles, assets, or behavior.
- Describe domain state in [data-model.md](./data-model.md), and validate the
  browser journeys using [quickstart.md](./quickstart.md).
- No backend, database, login, or external service contract is required.
