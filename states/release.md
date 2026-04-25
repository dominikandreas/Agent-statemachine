# release

Finalize a completed work unit.

## Intent
- clean up
- document
- leave repo in a sane state
- publish the result like a disciplined engineer, not like a raccoon leaving the kitchen

## Allowed actions
- refresh documentation
- move / remove temporary artifacts
- update task board
- update memory
- summarize accepted result
- update `Changes.md`
- git commit
- git push
- prepare the next queued planning item

## Not allowed
- new feature work
- new debugging branch

## Required outputs
- cleanup completed or explicitly deferred
- docs updated or explicitly deferred
- backlog / task board updated

## Typical next states
- `cleanup_and_refactoring`
- `refactoring` when the release is done but the fresh code shape clearly wants bounded structural simplification before more feature growth

## Release checklist
- temp / debug artifacts classified or removed
- docs touched if behavior / structure changed
- `Changes.md` updated
- git commit created
- git push completed
- next task recorded
- no hidden experimental leftovers
