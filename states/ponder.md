# ponder

Step back and think at the high level.

## Intent
- reflect roughly once per day
- review what changed since the last `ponder`
- reconnect daily activity to higher-level goals
- notice drift, neglected priorities, or repeated loops
- allow some mental wandering so adjacent ideas, odd patterns, and off-track-but-interesting threads can surface before they are prematurely crushed into a task
- consolidate or clean up task tracking, check what has been done but not marked as such, and update a completion log if the repo uses one

## Allowed actions
- read recent `memory/YYYY[-MM[-DD]].md` entries
- read `memory/heartbeat_state.json`
- read current task or planning artifacts
- summarize progress, direction, and risks
- write one short strategic note or recommendation
- briefly follow a surprising tangent if it helps reveal drift, opportunity, or a better framing

## Not allowed
- slipping into implementation
- broad diagnostics without synthesis
- turning reflection into a vague essay with no conclusion

## Required outputs
- what changed since the last `ponder`
- current high-level goals
- whether recent actions are still serving the main objective, or whether local optimization, cleanup, or curiosity started replacing goal progress
- one observed drift, risk, or opportunity
- one recommended next emphasis
- what deserves less focus now

## Reply contract
- `ponder` must not receive a forced `TARGET` as input context
- `ponder` is not a worker state receiving a scoped assignment
- it may emit a `TARGET` if reflection naturally crystallizes into one concrete next focus
- it may wander a bit before converging, but it must still end with a useful synthesis or steering observation

## Typical next states
- `planning`
- `inspection_and_ideation`
- `cleanup`
- `refactoring` if reflection surfaced one clear complexity seam worth simplifying next
