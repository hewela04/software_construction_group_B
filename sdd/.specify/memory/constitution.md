# Battleship Game Constitution

## Core Principles

### I. Simple, Maintainable Code
Implementation must favor clear, readable code that is easy to maintain. Keep the design appropriate to a small browser game; avoid unnecessary complexity and abstractions. Add comments where non-obvious or complex logic benefits from explanation.

### II. Specification Fidelity
Implement the Battleship requirements delivered by the project workers. Treat the agreed specifications as the source of truth for game behavior. Any proposed change to a stated requirement must be reviewed and documented before it is adopted.

### III. Verified Game Rules
Essential game rules and functionality must be verified against the specification using automated tests or manual checks, depending on what is practical for this student project. Verification should cover invalid ship placements, hits and misses, win and loss conditions, and restarting the game. 

### IV. Browser-First Scope
The game must run in a web browser. It does not require a backend, database, or login; do not introduce these dependencies unless the project requirements are formally reviewed and changed.

### V. Reviewable Changes
Keep changes focused and consistent with the existing implementation. Review changes for specification compliance, maintainability, and adequate test coverage before considering them complete.

## Technical Constraints

- Deliver a browser-based game without requiring a backend service, persistent database, or user authentication.
- Keep game behavior aligned with the documented Battleship requirements.
- Avoid adding infrastructure or dependencies that are not justified by an approved requirement.

## Development and Quality Workflow

- Consult the current specifications before implementing or changing game behavior.
- When requirements change, record the change and its review so implementation and tests can be updated consistently.
- Validate rule changes with tests that exercise the relevant outcomes, including invalid placements, hits, misses, win/loss, and restart behavior where applicable.
- Verify that the delivered game runs in a browser and that changes preserve existing specified behavior.

## Governance

This constitution guides project implementation and review. The Battleship specifications define detailed game behavior and must remain consistent with these principles. Proposed amendments to this constitution or to agreed requirements must be reviewed and documented; update the constitution version and amendment date when it changes. Changes must not silently weaken the browser-only scope or required rule verification.

**Version**: 1.0.0 | **Ratified**: 2026-10-21 | **Last Amended**: 2026-10-21
