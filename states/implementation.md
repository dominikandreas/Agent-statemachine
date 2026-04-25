# implementation

Perform one bounded engineering change.

## Intent
- execute one concrete work unit
- keep the change narrow, reversible, and reviewable
- validate the result before moving on

## Allowed
- edit code, docs, or config
- add or update tests
- run one bounded validation sequence
- do at most one tiny immediate fix for a trivial integration breakage

## Not allowed
- a second unrelated fix
- architecture rewrite without prior planning
- repeated speculative patch loops
- a new feature without a test when a test is practical

## Required output
- exact files changed
- exact command(s) run
- pass or fail result
- if nothing changed, execution evidence or an explicit freeze or user-decision path

## Rules
- If no real blocker exists, implementation must include at least one step that moves the work.
- No-op implementation replies without blocker are invalid.
- If the first validation shows conceptual failure or more than one real fix attempt would be needed, stop and hand off.
- If the work turns out to be mostly structural simplification, hand off to `refactoring`.

## Typical next states
- `review`
- `refactoring`
- `planning`
