# HEARTBEAT.md

## Status
Heartbeat is for useful bounded work, guided by explicit states.

If there is no concrete queued implementation or planning target, fall back to reflection or planning instead of idling.

## Usefulness invariant
Every heartbeat should do at least one of these in a meaningful way:
1. make material progress on a work unit
2. reduce uncertainty enough to change the next action
3. obtain a required human decision
4. explicitly freeze or close a work unit
5. perform strategic steering that changes priorities or execution direction

State compliance alone is not enough.

## Purpose
Heartbeat is a bounded state machine, not an open-ended autonomous loop.

Authoritative design:
- `states/HEARTBEAT_STATE_MACHINE.md`

## First step
1. Read `TOOLS.md` if relevant
2. Read `states/HEARTBEAT_STATE_MACHINE.md`
3. Read `memory/heartbeat_state.json` if it exists
4. Before executing a queued/current state, read `states/<state>.md`

## State machine rule
Each heartbeat should have one primary state at a time.
A single heartbeat may execute multiple sequential states when the next state is obvious, safe, and bounded.

If the current state is unclear, fall back to `planning` or `ponder`.

## State source
Use `memory/heartbeat_state.json` as the runtime source of truth when present.

Suggested fields:
- `enabled`
- `current_state`
- `next_state`
- `target`
- `acceptance`
- `task_ref`
- `last_result`
- `last_manager_at`
- `last_sprint_plan_at`
- `sprint_due_at`
- `updated_at`

## Safety rails
Stop and hand off instead of looping when:
- repeated implementation attempts are failing
- architecture redesign is required
- the task spills across multiple layers unexpectedly
- validation failure is global instead of local
- the next sensible action is ambiguous
- the work has become open-ended exploration

No patch spiral.

## Engineering rules
- Prefer test-driven implementation when practical.
- New features should include at least one test.
- Review should verify the relevant tests and checks.
- Review should also inspect ownership boundaries, documentation drift, and leftover artifacts.

## Suggested reply format for active states
- `STATE`
- `CHANGED`
- `VALIDATION`
- `RESULT`
- `NEXT_STATE`
- `BLOCKER`

## End condition
At the end of an active heartbeat:
1. update `memory/YYYY-MM-DD.md` when useful
2. update `memory/heartbeat_state.json` if the state changed

If there is no queued work but active goals still exist, prefer reflection, planning, review, cleanup, or an explicit freeze/handoff over idling.
