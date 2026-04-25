# review

Check what changed and whether it is acceptable.

## Intent
- verify correctness
- catch drift, leftovers, and broken ownership
- decide whether to release, fix, or rethink

## Allowed
- run tests or checks
- inspect diffs, docs, and artifacts
- identify wrong-layer, duplicate, or deprecated paths
- record findings

## Not allowed
- broad new implementation work

## Required output
- `VERDICT`: pass, pass-with-followup, or fail
- exact findings

## Checklist
- do the relevant tests pass?
- are tests aligned with the intended behavior?
- does code live in the correct layer?
- are docs current enough?
- did we create junk or dead paths?
- is `refactoring` the honest next step for this change?
- if `last_refactor_at` is missing, stale, or there has been substantial work since the last refactor, inspect the broader codebase for 1-3 concrete refactor candidates instead of only reviewing the local diff

## Correction rule
- If the review was attached to the wrong work unit, wrong state, or wrong conclusion, fix the affected memory or state files before replying.

## Typical next states
- `release`
- `implementation`
- `refactoring`
- `planning`

## Refactor trigger hints
A broader refactor scan is warranted when one or more of these are true:
- `last_refactor_at` is missing
- `work_units_since_refactor` is high for this repo
- several recent work units touched the same area
- ownership boundaries are getting blurry even though tests still pass
- review keeps finding duplicate logic, awkward seams, or repeated cleanup leftovers
