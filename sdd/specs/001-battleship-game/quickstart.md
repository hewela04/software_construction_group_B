# Quickstart: SDD Battleship Game

## Scope and prerequisites

This guide validates the independent implementation to be created at
`sdd/battleship.html`. It is not a guide to the root-level game. Implement and
validate the SDD file using only the SDD constitution and
[feature specification](./spec.md); do not copy, import, or reuse the root
game's code, styles, assets, or behavior.

After implementation, use a current desktop or mobile browser with JavaScript
enabled. No account, backend, or database is required.

## Run the SDD implementation

Open `sdd/battleship.html` in a browser. Alternatively, start any static file
server rooted at `sdd/` and open its `battleship.html` page. Confirm the address
and loaded document belong to the SDD folder.

## Acceptance validation

Run the scenarios against the SDD-local game in a fresh match, restarting
between scenarios where useful. These checks follow the SDD requirements and
constitution.

### Setup and fleet placement

1. Confirm the page title is **Battleship** and both boards show columns A-J
   and rows 1-10 with clear human/computer identification.
2. Confirm starting is unavailable until all five human ships have valid
   placements.
3. Select an unplaced ship and orientation, then preview proposed cells before
   confirmation.
4. Attempt an out-of-bounds placement and an overlapping placement. Confirm
   each is rejected without changing the existing fleet.
5. Confirm a ship ending exactly at an edge is accepted, and ships may touch
   along an edge or corner without overlapping.
6. Complete the fleet and verify one length-4 battleship, one length-3 cruiser,
   one length-3 destroyer, and two length-2 submarines.
7. Randomize the human fleet. Verify all five required ships are present,
   straight, in bounds, and non-overlapping.
8. Verify the computer receives a legal randomized fleet and its unhit ships
   remain hidden from the human.

### Turns, shots, and sinking

1. Start play with valid fleets and verify the current turn is identified.
2. Target an unshot computer coordinate. Verify the correct hit or miss result,
   announcement, and specified visual marking.
3. Try to target that coordinate again. Verify a second shot is rejected and
   the original result is unchanged.
4. After a non-terminal human shot, verify the computer targets a coordinate
   it has not previously shot, reports hit or miss, and yields the turn back.
5. Sink a ship and verify it is clearly distinguished and an announcement
   states that a computer ship has been sunk. Other unhit computer ships must
   remain hidden.
6. Verify the computer's unhit human ships remain visible on the human board.

### Game end and restart

1. In one match, sink every computer ship. Verify the exact message
   **“Congrats, you won!”**, immediate end of play, and rejection of further
   shots.
2. In a separate match, allow the computer to sink every human ship. Verify the
   exact message **“Game over! Computer wins.”** and rejection of further shots.
3. Restart during setup, active play, and after a finished match. Verify shots,
   marks, announcements, and results are cleared; the game returns to setup;
   the human must place ships again; and the computer receives a new randomized
   fleet.
4. Verify **Play again** after a result produces the same fresh setup state as
   **Restart**.

### Responsive layout and interaction

- At a viewport where both boards fit, verify they appear side by side; at a
  smaller viewport, verify they can be viewed stacked without losing controls.
- Verify setup, targeting, and restart interactions work with the input methods
  supported by the interface, including keyboard interaction.

## Validation record

Record the browser and viewport used, scenarios passed or failed, and any
specification discrepancies when carrying out validation. Automated tests may
supplement these checks if established within the SDD project, but must target
the SDD implementation and verify behavior from the specification.
