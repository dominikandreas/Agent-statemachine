# cleanup

Cleanup, archive, and repo stewardship without product-logic changes.

This state is for standalone hygiene work. If the work is happening because an accepted change is being finalized for shipping, that belongs in `release` instead.

## Intent
- keep the repo healthy between deep-work cycles
- archive artifacts and classify stale leftovers
- identify files that could be removed
- avoid turning the state into low-value cache-janitor theater

## Allowed actions
- lightweight checks
- import or path sanity
- repo structure checks
- stale artifact detection
- archive candidate detection
- doc drift detection
- dependency or test command sanity
- bounded cleanup stewardship
- when cleanup or archive work touches a structured data area, read and follow any repo-specific data lifecycle spec if one exists

## Not allowed
- policy or environment logic changes
- large file moves unless explicitly planned
- broad repo archaeology when classification is ambiguous
- destructive cleanup of files whose ownership or value is unclear
- disguising feature work as cleanup
- structural refactoring that needs real design judgment, file surgery, or architectural simplification work

## Cleanup rule
- prefer work that improves artifact hygiene, repo clarity, and leftover classification
- if the task turns into "this codebase shape should be simplified" rather than "this leftover should be cleaned", move to `refactoring` or `planning`
- if cleanup needs historical investigation or touches many files or trees, stop and move to `planning`

## Required outputs
- short cleanup report
- if cleanup happened, exactly what was archived, removed, or classified
- if no cleanup happened, say so plainly
- if a structural improvement opportunity was found, name the strongest concrete one and queue `refactoring` or `planning`

## Typical next states
- `refactoring` if one bounded structural improvement seam is now obvious
- `ponder` if no concrete cleanup task remains but active goals still exist
- `planning` if one concrete next task exists but still needs shaping
