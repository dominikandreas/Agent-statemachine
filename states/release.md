# release

Finalize a completed work unit.

## Intent
- clean up
- document
- leave the repo in a sane state
- publish the result like a disciplined engineer, not like a raccoon leaving the kitchen

## Allowed actions
- refresh documentation
- move or remove temporary artifacts
- update task board
- update memory
- summarize accepted result
- update changelog or release notes if the repo uses them
- git commit
- git push if publishing or pushing was already authorized for this work unit
- prepare the next queued planning item

## Not allowed
- new feature work
- new debugging branch

## Required outputs
- cleanup completed or explicitly deferred
- docs updated or explicitly deferred
- backlog or task board updated
- release or publish status made explicit

## Typical next states
- `cleanup`
- `refactoring` when the release is done but the fresh code shape clearly wants bounded structural simplification before more feature growth

## Release checklist
- temp or debug artifacts classified or removed as part of shipping this accepted work unit
- docs touched if behavior or structure changed
- changelog or release notes updated if the repo uses them
- git commit created
- git push completed if push was authorized
- next task recorded
- no hidden experimental leftovers
