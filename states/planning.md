# planning

Turn a vague direction into one bounded work unit.

## Intent
- define the exact next seam
- define acceptance and validation
- remove ambiguity before coding

## Allowed
- inspect docs, repo structure, tasks, memory, and artifacts
- create or update one plan artifact
- write or update the next queued state

## Not allowed
- implementation work

## Required output
- `TARGET`
- `ACCEPTANCE`
- `VALIDATION`
- `NEXT`

## Rules
- If you can name a concrete seam and validation path, do not loop into `planning` again.
- Another `planning` outcome is only honest when you need a binary decision, an explicit freeze, or a handoff to `manager`.
- If the work unit is purely structural, queue `refactoring`.

## Typical next states
- `implementation`
- `refactoring`
- `review`
- `manager`
