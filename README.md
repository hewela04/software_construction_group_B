# software_construction_group_B

How to run the project:

Download or copy the battleship.html file and open in an optional development environment with Python, e.g. PyCharm.

Project summary:

In this project we built a battleship game in which a player competes against a computer opponent. The game includes for example ship placement, hit and miss detection, turn-based attacks and responsive user interface. The system was developed using HTML5, CSS3 and vanilla JavaScript. The system does not require a backend, database or user authentication. We used semi-formal specification techniques, primarily natural language requirements, function and non-functional requirements, user stories, interface descriptions and structured development tasks. The requirements defined the expected game behavior, constraints and quality attributes. We did not use any formal mathematical specification languages. 

We used two different AI agents for the project. We used Claude (Opus 5.5) for the vibe coding to generate and refine the initial game implementation. For the specification-driven development (SDD) implementation, we used GitHub Copilot in Visual Studio Code. GitHub Desktop supported version control, while PyCharm and Firefox were used during the initial implementation and testing.

Our SDD workflow followed GitHub Spec Kit, progressing through /speckit-constitution, /speckit-specify, /speckit-plan and /speckit-tasks followed by /speckit-implement for individual tasks and /speckit-converge to identify inconsistencies between specifications, tasks and implementation. The work was tracked through Git commits, linking implementation changes to specific tasks.

Verification and validation combined AI-assisted JavaScript syntax checks using node –-check, automated gameplay tests, simulations of 2,000 games per difficulty level in Node.js, browser simulations and manual testing in Firefox. Twelve tests were reported, including eight automated or semi-automated tests and four manual tests, all passed, with two passing after fixes. These checks assessed gameplay rules, invalid ship placements, repeated attacks, difficulty differences, interface behavior and restart functionality. 

