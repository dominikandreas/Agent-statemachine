# refactoring

Simplify structure so future work stays cheaper, clearer, and less tangled.

## Intent
- reduce complexity before it hardens into policy spaghetti
- split files or modules that are too large or own too many concerns
- remove dead code when removal needs real checking rather than obvious trash pickup
- improve boundaries, naming, ownership, and structure without hiding feature work inside "cleanup"
- make growth easier after a release while context is still fresh

## Allowed actions
- inspect file size / function size / ownership seams
- split modules or helpers
- remove dead code after verifying it is actually dead
- simplify control flow, boundaries, and duplicated logic
- make bounded architectural improvements that do not change the product goal
- add / update tests needed to protect the refactor
- run bounded validation

## Not allowed
- broad redesign with no bounded seam
- sneaking in unrelated product features
- open-ended codebase beautification
- speculative rewrites with no clear complexity payoff
- changing behavior accidentally and calling it a refactor

## Refactoring rule
- start from one concrete complexity problem
- name what should get simpler
- keep the seam bounded and reviewable
- if the work expands into architecture strategy or multiple competing options, stop and move to `planning` or `manager`

## Good triggers
- a file is too long or mixes concerns
- dead code removal needs proof, not just deletion bravado
- a recent release left structure that works but will age badly
- repeated implementation pain points point to one ownership or complexity seam

## Required outputs
- exact complexity / ownership problem being reduced
- exact files changed
- exact validation run
- blunt statement of what became simpler

## Typical next states
- `review` if the refactor landed cleanly
- `planning` if the structural seam is larger than expected
- `ponder` if the simplification raised a broader strategic question
