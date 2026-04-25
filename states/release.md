# release

Finalize an accepted work unit.

## Intent
- do the shipping cleanup
- refresh docs if needed
- leave the repo in a sane releasable state

## Allowed
- summarize the accepted result
- refresh docs or changelog if the repo uses them
- clean temporary artifacts related to the accepted work
- commit
- push if publishing was already authorized
- record the next task

## Not allowed
- new feature work
- new debugging branches

## Required output
- cleanup status
- docs status
- publish status
- next task status

## Typical next states
- `cleanup`
- `refactoring`
