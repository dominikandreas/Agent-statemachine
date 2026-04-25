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
- is `refactoring` the honest next step?

## Correction rule
- If the review was attached to the wrong work unit, wrong state, or wrong conclusion, fix the affected memory or state files before replying.

## Typical next states
- `release`
- `implementation`
- `refactoring`
- `planning`
