# cleanup

Standalone repo hygiene without product-logic changes.

## Intent
- clean leftovers, archive artifacts, and keep the repo sane
- classify stale files and obvious cleanup candidates
- stop when the work turns into structural redesign

## Allowed
- path or import sanity checks
- stale artifact detection
- archive candidate detection
- doc drift checks
- bounded cleanup work

## Not allowed
- feature work
- broad archaeology
- destructive cleanup when ownership is unclear
- structural changes that really belong in `refactoring`

## Required output
- what was cleaned, archived, removed, or classified
- or a plain statement that no cleanup happened
- strongest structural follow-up, if the work surfaced one

## Typical next states
- `refactoring`
- `planning`
- `ponder`
