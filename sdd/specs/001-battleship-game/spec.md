# Feature Specification: Browser Battleship Game

**Feature Branch**: `main`

**Created**: 2026-10-21

**Status**: Draft

**Input**: User description: Create a browser-based Battleship game where one human plays against a computer, places a fleet, takes turns firing, sees hit/miss and sinking results, and can restart.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Set Up the Fleet (Priority: P1)

As a player, I want to place my ships on my board before play so that I can choose my own fleet layout and begin a fair game against the computer.

**Why this priority**: The game cannot begin until both fleets have legal placements. Manual placement is the first required player journey.

**Independent Test**: Place the complete fleet legally, verify that invalid placements are rejected without changing the board, and verify that the game can start only after all five ships are placed.

**Acceptance Scenarios**:

1. **Given** a new game, **When** the player views the setup screen, **Then** two 10-by-10 boards are shown with columns A-J and rows 1-10, along with controls to choose a ship and its horizontal or vertical orientation.
2. **Given** an unplaced ship is selected, **When** the player previews a placement, **Then** the proposed occupied squares are previewed before confirmation.
3. **Given** a proposed placement that overlaps another ship or extends beyond the board, **When** the player attempts to confirm it, **Then** the placement is rejected and the board remains unchanged.
4. **Given** a proposed placement that is straight, fits within the board, and does not overlap another ship, **When** the player confirms it, **Then** the ship is placed; it may touch other ships.
5. **Given** fewer than five ships have been legally placed, **When** the player views the setup controls, **Then** starting the game is unavailable.
6. **Given** all five ships have been legally placed, **When** the player views the setup controls, **Then** starting the game is available.
7. **Given** the player chooses to randomize their fleet, **When** the random placement completes, **Then** all five ships are placed legally and the player can still restart setup or start the game.

### User Story 2 - Play and Finish a Game (Priority: P1)

As a player, I want to take turns firing at the computer's fleet and see the outcome of every shot so that I can try to sink all of its ships and know when the game is over.

**Why this priority**: Turn-based play and a clear win or loss are the central purpose of Battleship.

**Independent Test**: Start with valid fleets, exercise hits, misses, repeat-shot rejection, ship sinking, both terminal outcomes, and verify that the computer's unhit ships remain hidden.

**Acceptance Scenarios**:

1. **Given** both fleets are placed and the game has started, **When** the player views the game, **Then** the boards are side by side when space allows and may stack on smaller screens, the computer's unhit ships are hidden, and the current turn is identified.
2. **Given** it is the player's turn and a computer-board square has not been targeted, **When** the player selects that square, **Then** the square is marked as a hit in red if it contains a ship or as a miss in blue/grey otherwise, and the corresponding “hit” or “miss” result is shown.
3. **Given** a square has already been targeted, **When** the player tries to target it again, **Then** the shot is not accepted and the existing result remains unchanged.
4. **Given** a shot hits the last unhit square of a ship, **When** the result is shown, **Then** the sunk ship is clearly distinguishable and a message announces that one of the computer's ships has been sunk.
5. **Given** the game is active after a non-terminal player shot, **When** the computer takes its turn, **Then** it randomly selects a square on the human board that it has not previously targeted and shows the hit or miss result.
6. **Given** all computer ships have been sunk by the player, **When** the final hit is resolved, **Then** play ends and “Congrats, you won!” is shown without another computer shot.
7. **Given** all human ships have been sunk by the computer, **When** the final hit is resolved, **Then** play ends and “Game over! Computer wins.” is shown.
8. **Given** the game is over, **When** either player board is selected, **Then** no further shot is accepted.

### User Story 3 - Restart and Play Again (Priority: P2)

As a player, I want to restart the game so that I can begin a fresh match and manually place my ships again.

**Why this priority**: Restarting makes the game reusable after a match and lets a player abandon an unfinished setup or game.

**Independent Test**: Restart from setup, an active match, and a finished match; verify shots and outcomes are cleared, the human fleet must be placed again, and the new match starts in setup.

**Acceptance Scenarios**:

1. **Given** setup, an active game, or a completed game, **When** the player selects “Restart”, **Then** all shots, hit/miss marks, announcements, and game results are cleared and setup begins again.
2. **Given** the player restarts, **When** the new setup is shown, **Then** the human's ships must be placed manually again and a new computer fleet is automatically randomized.
3. **Given** a game has ended, **When** the player selects “Play again”, **Then** the same fresh setup state as “Restart” is shown.

### Edge Cases

- A ship whose end lies exactly on an edge of the board is a legal placement; a ship extending even one square beyond an edge is not.
- Ships may touch along an edge or at a corner, but two ships may not occupy the same square.
- The player may not start with an incomplete fleet or an invalid ship placement.
- A random fleet placement must contain every required ship, must fit within the board, and must not overlap.
- The computer must never select a square it has already targeted, including when only one unshot square remains.
- A final winning or losing hit ends the game immediately; the other side must not take another turn.
- Restarting clears all prior results, including sunk-ship announcements, and allows a new complete match.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: The game MUST support one human player against one computer opponent in a browser, without requiring login, a backend, or a database.
- **FR-002**: The game MUST present one human board and one computer board, each containing 100 squares arranged in 10 columns and 10 rows. Columns MUST be labeled A-J and rows MUST be labeled 1-10.
- **FR-003**: The interface MUST present the boards side by side when screen space permits and MUST allow them to stack on smaller screens.
- **FR-004**: Each side MUST have a fleet of exactly five straight ships: one length-4 battleship, one length-3 cruiser, one length-3 destroyer, and two length-2 submarines.
- **FR-005**: Each ship MUST occupy consecutive squares in one horizontal or vertical orientation, remain entirely within its board, and not overlap another ship. Ships MAY touch other ships.
- **FR-006**: Before play, the human MUST be able to select each unplaced ship, choose its placement and orientation, preview its proposed squares, and confirm a legal placement.
- **FR-007**: The game MUST reject illegal human placements, including placements outside the board and placements that overlap another ship, without altering the existing fleet.
- **FR-008**: The human MUST be able to randomize their fleet. The resulting fleet MUST include all five required ships and satisfy all placement rules.
- **FR-009**: The game MUST make starting available only after all five human ships have been legally placed.
- **FR-010**: Before play begins, the computer MUST automatically receive a randomized fleet containing all five required ships and satisfying all placement rules.
- **FR-011**: Before play, the human MUST be able to see their own fleet but MUST NOT be able to see the computer's ships.
- **FR-012**: Once both fleets are ready and the human starts the game, the game MUST alternate turns between the human and the computer, identify whose turn it is, and show the current game status.
- **FR-013**: On the human's turn, the human MUST be able to target a square on the computer board that has not previously been targeted.
- **FR-014**: The game MUST reject a shot at any square previously targeted by that player.
- **FR-015**: For every accepted shot, the game MUST report “hit” if a ship occupies the targeted square and “miss” otherwise.
- **FR-016**: Accepted hits MUST be marked red and accepted misses MUST be marked blue/grey on the targeted board.
- **FR-017**: On the computer's turn, the computer MUST randomly select an unshot square on the human board and report the resulting hit or miss.
- **FR-018**: The game MUST identify a ship as sunk once all of its squares have been hit and MUST clearly distinguish the sunk ship and announce that a ship has been sunk.
- **FR-019**: The human's undamaged computer ships MUST remain hidden. The computer's unhit human ships remain visible on the human board.
- **FR-020**: After each accepted shot, the game MUST determine whether every ship on either side has been sunk. If all computer ships are sunk, it MUST end the game and show “Congrats, you won!” If all human ships are sunk first, it MUST end the game and show “Game over! Computer wins.”
- **FR-021**: Once the game ends, the game MUST reject all further shots until it is restarted.
- **FR-022**: A “Restart” control MUST be available during setup and play. Selecting it MUST clear all shots and game results, return to setup, require the human to place all ships manually again, and create a new randomized computer fleet.
- **FR-023**: After a game ends, a “Play again” control MUST be available and MUST start the same fresh setup state as “Restart”.
- **FR-024**: The interface MUST have the title “Battleship” and clearly identify the human board and the computer board.

### Key Entities

- **Board**: One side's 10-by-10 set of squares, with coordinates A-J and 1-10, ship placements, and shot results.
- **Ship**: A named fleet member with a fixed length, straight placement, orientation, and hit state for each occupied square.
- **Fleet**: The five ships belonging to one side, with placement and sunk status.
- **Shot**: A targeted board coordinate, its firing side, and its hit or miss result; a coordinate may be targeted only once per side.
- **Game**: The match state, both fleets, current turn, shot history, status announcements, and win/loss outcome.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: A completed setup contains exactly five ships per side with lengths 4, 3, 3, 2, and 2, and every ship is straight, in bounds, and non-overlapping.
- **SC-002**: Every attempted out-of-bounds or overlapping manual placement is rejected, while edge-touching and corner-touching placements are accepted.
- **SC-003**: In rule verification, every accepted shot produces the correct hit or miss result and color, and no square can be accepted as a shot twice by the same side.
- **SC-004**: Sinking a ship produces a distinct visual indication and announcement; sinking the final opposing ship produces the specified terminal message and prevents further shots.
- **SC-005**: The computer completes each non-terminal turn by choosing an unshot square, and its unhit ships are never revealed to the human.
- **SC-006**: Restart and play again each clear all previous shots and outcomes and return the game to manual human fleet setup.
- **SC-007**: The complete setup, play, and restart journeys can be completed in a browser without login, backend service, or database.
- **SC-008**: Both boards show all required coordinates and are side by side when space permits; on smaller screens they can be viewed stacked without losing access to game controls.

## Assumptions

- A confirmed human shot is followed by a computer shot unless that human shot ends the game; there are no bonus turns for hits.
- “Restart” is available during setup, during play, and after the game; “Play again” is available after a win or loss and has the same reset behavior.
- A sunk computer ship is revealed only to the extent needed to make that sunk ship visually clear; other unhit computer ships remain hidden.
- The computer's randomized placement and shot choices need not be reproducible between games.
- The browser game is usable on both large and small screens; no specific screen-size breakpoint is prescribed.
