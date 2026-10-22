---
description: "Dependency-ordered implementation tasks for the SDD Battleship game"
---

# Tasks: Browser Battleship Game

**Input**: Design documents in `sdd/specs/001-battleship-game/`

**Prerequisites**: `sdd/specs/001-battleship-game/plan.md`,
`sdd/specs/001-battleship-game/spec.md`,
`sdd/specs/001-battleship-game/research.md`,
`sdd/specs/001-battleship-game/data-model.md`, and
`sdd/specs/001-battleship-game/quickstart.md`

**Implementation boundary**: Create the independent game in
`sdd/battleship.html`, using only the SDD constitution and feature
specification as authorities. Do not modify, copy, import, adapt, or reuse code,
styles, assets, or behavior from the root-level `battleship.html`.

**Tests**: The feature specification does not require a test-driven approach or
automated test framework. Do not add test infrastructure solely for this
feature. Validate the implementation against the browser scenarios in
`sdd/specs/001-battleship-game/quickstart.md`.

**Organization**: Tasks are grouped by the three user stories in the
specification. Story implementation tasks all target the same standalone HTML
file, so they are ordered and not marked parallelizable.

## Phase 1: Setup

**Purpose**: Establish the isolated SDD-local browser application target.

- [x] T001 Create a new standalone HTML document at `sdd/battleship.html` with a valid document structure, UTF-8 and responsive viewport metadata, page title “Battleship”, and no imports or references to files outside `sdd/`.

## Phase 2: Foundational

**Purpose**: Define the shared game-domain rules and state required by all user stories.

- [x] T002 Define the game data and coordinate rules in `sdd/battleship.html`: two 10-by-10 boards with columns A-J and rows 1-10; human and computer participants; and the five required ships per fleet with lengths 4, 3, 3, 2, and 2.
- [x] T003 Implement shared fleet-placement validation and randomized fleet creation in `sdd/battleship.html`; require straight horizontal or vertical ships that remain in bounds and do not overlap, while allowing ships to touch.
- [x] T004 Define match lifecycle state in `sdd/battleship.html` for setup, active play, and finished play, including participant boards, current turn, shot history, ship hit/sunk state, and winner; keep match data in browser memory without a backend or database.

**Checkpoint**: The standalone file and shared game rules are ready for the independently verifiable user-story work.

## Phase 3: User Story 1 - Set Up the Fleet (Priority: P1)

**Goal**: Let the player prepare a legal fleet and start only when all five ships have been placed.

**Independent Test**: In a new SDD game, place a complete fleet legally, verify out-of-bounds and overlapping proposals are rejected without changing the board, verify edge/corner touching is allowed, and confirm starting is unavailable until all five ships are legally placed.

### Implementation

- [x] T005 [US1] Render two identified 10-by-10 boards with column labels A-J and row labels 1-10, plus setup controls for selecting each unplaced ship and choosing horizontal or vertical orientation, in `sdd/battleship.html`.
- [x] T006 [US1] Implement human ship-placement preview and confirmation in `sdd/battleship.html`; show proposed occupied squares before confirmation and reject out-of-bounds or overlapping placements without changing any existing ship.
- [x] T007 [US1] Implement human fleet randomization in `sdd/battleship.html`; generate exactly one length-4 battleship, one length-3 cruiser, one length-3 destroyer, and two length-2 submarines in legal, non-overlapping positions.
- [x] T008 [US1] Gate the start control in `sdd/battleship.html` until all five human ships are legally placed; on start, ensure the computer has its own legal randomized fleet, show the human's ships, conceal the computer's unhit ships, and enter active play.

**Checkpoint**: The player can complete setup, inspect the two labeled boards, and enter play only with a complete legal fleet.

## Phase 4: User Story 2 - Play and Finish a Game (Priority: P1)

**Goal**: Support alternating shots, understandable results, sinking announcements, and immediate win/loss outcomes.

**Independent Test**: Start with legal fleets, verify hits and misses and their colors, reject repeated shots, verify the computer selects only unshot coordinates, sink ships, verify both terminal outcomes and exact messages, and confirm no shots are accepted after game end.

**Dependency**: Requires User Story 1 to produce valid fleets and enter active play.

### Implementation

- [x] T009 [US2] Implement turn identification and human targeting in `sdd/battleship.html`; allow targeting only an unshot computer-board coordinate during the human turn and reject repeated or out-of-turn shots.
- [x] T010 [US2] Resolve each accepted shot in `sdd/battleship.html` as a hit or miss, record its result once, visibly mark hits red and misses blue/grey, and announce the corresponding result.
- [x] T011 [US2] Implement the computer turn in `sdd/battleship.html`; after each non-terminal human shot choose a random unshot coordinate on the human board, report hit or miss, and return the turn to the human.
- [x] T012 [US2] Detect sunk ships and terminal outcomes in `sdd/battleship.html`; clearly distinguish and announce a sunk ship, show exactly “Congrats, you won!” when all computer ships are sunk or “Game over! Computer wins.” when all human ships are sunk, and reject further shots after either outcome.

**Checkpoint**: A complete match can be played to either terminal outcome with correct shot feedback and no repeated or post-game shots.

## Phase 5: User Story 3 - Restart and Play Again (Priority: P2)

**Goal**: Start a fresh manual setup from setup, active play, or a completed game.

**Independent Test**: Restart at each lifecycle phase and use Play again after a result; verify all shots and results are cleared, the human must place all ships again, and the computer receives a new randomized fleet.

**Dependency**: Requires User Story 1 setup state and User Story 2 active/finished states.

### Implementation

- [ ] T013 [US3] Add a Restart control available during setup, active play, and after a completed game in `sdd/battleship.html`; reset shots, hit marks, announcements, and outcome, return to manual human fleet setup, and create a new legal randomized computer fleet.
- [ ] T014 [US3] Add a Play again control after a win or loss in `sdd/battleship.html`; make it produce the same fresh setup state as Restart, including a cleared human fleet and a new legal computer fleet.

**Checkpoint**: Restart and Play again both return the game to a clean, playable setup without retaining results from the previous match.

## Phase 6: Polish and Cross-Cutting Validation

**Purpose**: Verify the full SDD-local experience against the specification.

- [ ] T015 Ensure the boards in `sdd/battleship.html` display side by side when space permits and can stack on smaller screens without losing access to game controls.
- [ ] T016 Validate the SDD-local game by completing the setup, turn/shot, sinking, win, loss, and restart scenarios in `sdd/specs/001-battleship-game/quickstart.md`; record any failures and resolve specification deviations in `sdd/battleship.html`.

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies; creates the independent SDD-local game file.
- **Foundational (Phase 2)**: Depends on Setup; must finish before user-story tasks.
- **User Story 1 (Phase 3)**: Depends on the foundation; delivers the first usable setup increment and MVP.
- **User Story 2 (Phase 4)**: Depends on User Story 1 because active play requires complete legal fleets.
- **User Story 3 (Phase 5)**: Depends on User Stories 1 and 2 because restart and play again must cover setup, active, and finished states.
- **Polish (Phase 6)**: Depends on all user stories.

### User Story Dependencies

- **US1 (P1)**: Starts after Phase 2; no dependency on another user story.
- **US2 (P1)**: Starts after US1; it requires the setup journey to create valid fleets and start the match.
- **US3 (P2)**: Starts after US1 and US2; its independent test covers all three game lifecycle phases and a post-result replay.

### Task Dependencies

```text
T001 -> T002 -> T003 -> T004
                 |
                 v
T005 -> T006 -> T007 -> T008
                          |
                          v
T009 -> T010 -> T011 -> T012
                          |
                          v
T013 -> T014 -> T015 -> T016
```

The arrows indicate implementation prerequisites, not permission to share or
reuse code from the root-level game. All game implementation tasks operate on
`sdd/battleship.html`.

### Parallel Opportunities

There are no safe parallel implementation tasks within a user story: tasks
modify the same standalone file and later tasks rely on earlier behavior.
Separate contributors should work sequentially by phase rather than edit
`sdd/battleship.html` concurrently. Manual checks in the quickstart may be
distributed after the corresponding flows are implemented, but final
end-to-end validation follows all story phases.

## Parallel Example

```text
US1: No parallel implementation tasks; complete T005, then T006, T007, and T008
US2: No parallel implementation tasks; complete T009, then T010, T011, and T012
US3: No parallel implementation tasks; complete T013, then T014
```

## Implementation Strategy

### MVP First (User Story 1)

1. Complete Setup and Foundational phases.
2. Complete User Story 1 to deliver a new standalone game page with legal fleet
   setup and a guarded start.
3. Stop and validate the US1 independent test before adding match play.

### Incremental Delivery

1. Complete US1 and verify fleet setup.
2. Complete US2 and verify turns, shot outcomes, sinking, and terminal states.
3. Complete US3 and verify reset/replay from setup, active play, and game over.
4. Complete responsive layout and all quickstart scenarios.

## Notes

- Every task uses the required checkbox, sequential task ID, optional
  parallel marker, story label when applicable, and an explicit file path.
- No automated-test or test-framework setup task is included because the
  specification does not request TDD or require a particular test framework.
- Keep every implementation and validation action within the SDD project and
  derive behavior from its constitution and specification.

## Phase 7: Convergence

- [ ] T017 Implement keyboard-operable board and game controls with a visible focus indicator in `sdd/battleship.html` per plan: keyboard access (missing).
