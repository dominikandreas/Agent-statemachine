# refactoring

Simplify structure so future work stays cheaper and clearer.

## Intent
- reduce one concrete complexity seam
- improve boundaries, naming, ownership, or duplication
- keep the seam bounded and reviewable

## Allowed
- split files or helpers
- remove verified dead code
- simplify control flow or ownership boundaries
- add tests needed to protect the refactor
- run bounded validation

## Not allowed
- broad redesign with no bounded seam
- sneaking in unrelated feature work
- behavior changes disguised as refactoring

## Required output
- exact complexity problem being reduced
- exact files changed
- exact validation run
- blunt statement of what became simpler
- if heartbeat memory is in use, the `last_refactor_at` and `last_refactor_summary` update that should be recorded

## Typical next states
- `review`
- `planning`
- `ponder`
