# planning

Convert a vague idea into a concrete next implementation unit.

## Intent
- define concrete tasks
- define acceptance
- remove ambiguity before coding

## Allowed actions
- read task board / recent memory / relevant docs
- inspect repo structure
- inspect latest metrics / artifacts
- create or update a plan artifact
- write / update the next queued state

## Not allowed
- implementation work

## Required outputs
- one concrete `TARGET`
- one concrete `ACCEPTANCE`
- one concrete `NEXT`

## Anti-stall rule (explicit)
Planning must not end in another `planning` state unless it is doing exactly one of these:
- asking the user for a binary decision that blocks safe progress
- freezing a work unit explicitly because no honest bounded implementation seam exists yet
- handing off to `manager` because the issue is actually priority/roadmap steering rather than task definition

If planning can name a concrete owner/file/function seam, acceptance, and validation path, it must queue `implementation` (or `review` if no coding is needed) instead of `planning` again.

Additional rule:
- two consecutive `planning` outcomes on the same work unit are a smell
- a third consecutive `planning` on the same work unit is not allowed unless new external information arrived or the user explicitly requested more design work

## Typical next states
- `implementation`
- `review` if no coding is needed
- `manager` if the real blocker is priority/strategy rather than task definition
