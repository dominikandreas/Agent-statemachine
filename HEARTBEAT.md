# HEARTBEAT.md

## Purpose
Heartbeat is for useful bounded work, guided by explicit states.
It is a bounded state machine, not an open-ended autonomous loop.

The authoritative design lives here:
- `states/HEARTBEAT_STATE_MACHINE.md`

If there is no concrete queued implementation or planning target, fall back to reflection, planning, cleanup, refactoring, or explicit freeze/handoff instead of idling.

## First step
1. Read `TOOLS.md` if relevant
2. Read `states/HEARTBEAT_STATE_MACHINE.md`
3. Read `memory/heartbeat_state.json` if this repo uses heartbeat memory and the file exists
4. Before executing a queued/current state, read `states/<state>.md`

## Operating rule
Each heartbeat should have one primary state at a time.
A single heartbeat may execute multiple sequential states when the next state is obvious, safe, and bounded.

If the current state is unclear, fall back to `planning` or `ponder`.

## Runtime state
If this repo uses heartbeat memory, use `memory/heartbeat_state.json` as the runtime source of truth.

Field definitions, reply contracts, and transition rules are defined in `states/HEARTBEAT_STATE_MACHINE.md`.

## Minimum bar
Every heartbeat should do at least one meaningful thing: make progress, reduce uncertainty, obtain a required decision, freeze or close work honestly, or change execution direction.

## Safety rails
Stop and hand off instead of looping when:
- repeated implementation attempts are failing
- architecture redesign is required
- the task spills across multiple layers unexpectedly
- validation failure is global instead of local
- the next sensible action is ambiguous
- the work has become open-ended exploration

No patch spiral.

## End condition
At the end of an active heartbeat:
1. update `memory/YYYY-MM-DD.md` when useful, if this repo uses memory
2. update `memory/heartbeat_state.json` if the state changed and this repo uses heartbeat memory

If there is no queued work but active goals still exist, prefer reflection, planning, review, cleanup, refactoring, or an explicit freeze/handoff over idling.
