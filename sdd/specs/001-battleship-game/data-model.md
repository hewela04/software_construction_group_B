# Data Model: Browser Battleship Game

## Scope

This domain model is derived from the SDD specification and is implementation
agnostic. It describes the information and invariants required for the
independent game to be created in `sdd/battleship.html`. It does not prescribe
particular classes, functions, libraries, or state-management mechanisms.

## Entities

### Game

Represents one match and its lifecycle.

| Concept | Allowed values or meaning |
|---|---|
| Phase | Setup, active play, or finished |
| Current turn | Human or computer while the game is active |
| Outcome | Human win, computer win, or no outcome yet |
| Participants | One human and one computer |
| Boards | One human board and one computer board |
| Announcements | Current shot/sinking/status feedback and terminal result |

**Invariants and transitions**

- A new game begins in setup.
- Active play can begin only after the human fleet is valid and the computer
  fleet has been randomized legally.
- Turns alternate after a non-terminal accepted shot.
- A terminal shot ends the game before the other participant takes another
  turn.
- A finished game accepts no additional shots.
- Restart or play again clears prior results and returns to setup, requiring
  the human to place ships again and assigning the computer a new randomized
  fleet.

### Board

Represents one participant's 10-by-10 grid.

| Concept | Allowed values or meaning |
|---|---|
| Owner | Human or computer |
| Coordinates | 10 columns A-J and 10 rows 1-10 |
| Fleet | Exactly five required ships |
| Received shots | Each targeted coordinate and its hit/miss result |

**Invariants**

- A board contains 100 distinct coordinates.
- A target coordinate can be shot at most once during a match.
- Once setup is complete, the fleet has the required composition and legal
  placements.
- The human can see their own ships. The computer's unhit ships are concealed;
  a sunk ship may be distinguished as allowed by the specification.

### Ship

Represents one straight fleet member.

| Concept | Allowed values or meaning |
|---|---|
| Type | Battleship, cruiser, destroyer, or submarine |
| Length | 4, 3, 3, or 2 cells respectively |
| Placement | Consecutive cells in one horizontal or vertical line |
| Hit state | Which occupied cells have been hit |
| Sunk state | All occupied cells have been hit |

**Fleet composition**: one length-4 battleship, one length-3 cruiser, one
length-3 destroyer, and two length-2 submarines.

**Placement invariants**

- Each ship has exactly its required number of cells.
- All cells are consecutive, in a single row or column, and within the board.
- No two ships occupy the same cell.
- Ships may touch along edges or corners.
- A ship is sunk exactly when every one of its cells has been hit.

### Shot

Represents an accepted attack on one board.

| Concept | Allowed values or meaning |
|---|---|
| Target | One board coordinate not previously targeted on that board |
| Attacker | The participant whose turn it is |
| Result | Hit if a ship occupies the target; otherwise miss |

An accepted hit updates the hit state of the occupying ship. The result must
be shown and the target marked with the specified hit or miss visual treatment.
If the hit sinks a ship, the game announces that event and clearly distinguishes
the sunk ship.

### Placement Proposal

Represents a temporary proposed location for a selected, unplaced human ship.

| Concept | Meaning |
|---|---|
| Ship | The fleet member being placed |
| Start coordinate | The first proposed board cell |
| Orientation | Horizontal or vertical |
| Occupied coordinates | The cells implied by start, orientation, and ship length |
| Validity | In bounds and does not overlap any placed ship |

A proposal is not part of the fleet until confirmed. Invalid confirmation
leaves the existing fleet unchanged. Randomized placement must produce the same
legal fleet composition and obey the same placement invariants.

## Relationships

- A `Game` contains exactly two `Board`s, one per participant.
- Each completed `Board` contains the required five `Ship`s.
- Each accepted `Shot` belongs to one attacker, one target board, and one
  coordinate.
- A shot result is determined by whether a ship occupies its target.
- A game outcome is determined by all ships on one board being sunk.

## Non-Goals

- No account, backend, database, or persistent match history is required.
- This model does not prescribe a UI layout implementation, programming
  abstractions, or storage technology beyond the browser-only scope in the
  constitution.
