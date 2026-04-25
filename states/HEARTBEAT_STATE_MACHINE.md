# HEARTBEAT_STATE_MACHINE.md

## Purpose
The heartbeat is a bounded state machine, not an open-ended autonomous coding loop.

Its job is to preserve quality, avoid drift, and make progress in small verified steps.

## Core principle
A heartbeat acts from **one primary state at a time**.
This does not mean one state per heartbeat. A single heartbeat may execute multiple sequential states as long as the current state is explicit and transitions stay honest.
If a state completes and the next state is clear and safe, continue in the same wake.

## Usefulness invariant (global)
Every heartbeat must do exactly one of these in a meaningful way:
1. make material progress on a work unit,
2. materially reduce uncertainty in a way that changes the next action,
3. obtain a required human decision,
4. explicitly freeze/close a work unit,
5. or perform strategic steering that changes priorities or execution direction.

State compliance does **not** justify a non-progress turn.
If a heartbeat produces none of the outcomes above, it is a failed heartbeat and must not repeat in the same shape.

Available states:
- `ponder`
- `manager`
- `inspection_and_ideation`
- `planning`
- `implementation`
- `review`
- `release`
- `cleanup_and_refactoring`
- `refactoring`
- `sleep`

## State summaries
Read this file first for global rules.
Before executing a specific state, read its detailed definition in `states/<state>.md`.

- `ponder`
  - high-level reflection and drift detection
  - details: `states/ponder.md`
- `manager`
  - strategic steering across goals, milestones, epics, and sprints
  - details: `states/manager.md`
- `inspection_and_ideation`
  - inspect current behavior and surface the next valuable idea
  - details: `states/inspection_and_ideation.md`
- `planning`
  - turn a vague direction into one bounded work unit
  - details: `states/planning.md`
- `implementation`
  - execute one bounded engineering change
  - details: `states/implementation.md`
- `review`
  - verify changes and decide whether they are acceptable
  - details: `states/review.md`
- `release`
  - finalize an accepted work unit cleanly
  - details: `states/release.md`
- `cleanup_and_refactoring`
  - repo stewardship, artifact cleanup, and leftover classification
  - details: `states/cleanup_and_refactoring.md`
- `refactoring`
  - bounded structural simplification and complexity reduction
  - details: `states/refactoring.md`
- `sleep`
  - memory consolidation
  - details: `states/sleep.md`

## Transition heuristics
Transitions are not a rigid workflow.
What matters is:
- the current primary state is explicit
- the reason for the next state is obvious
- the heartbeat does not drift into an unbounded loop
- the heartbeat does not stop early when a clear safe next state should obviously be executed now

### Good default heuristics
- move to `ponder` roughly once per day when a high-level reflection pass is due
- move to `manager` for milestone/epic/sprint steering, recurring sprint planning, end-of-sprint review against the strategic goals, or when sprint review is overdue
- if `sprint_due_at` exists and the current time is past due, prefer `manager` before local execution states unless a hard stop or urgent active incident justifies deviation
- move to `inspection_and_ideation` when active goals exist but the next concrete step is not ready yet
- move to `planning` when a candidate direction now needs to be turned into one concrete bounded task
- move to `implementation` when there is one concrete bounded change ready
- move to `review` after a meaningful change or when verification is due
- move to `release` when the work is accepted and only cleanup / docs / task updates remain
- move to `cleanup_and_refactoring` for repo hygiene, artifact cleanup, and leftover classification
- move to `refactoring` when one bounded structural simplification seam is obvious, especially after a release or repeated implementation pain on the same ownership boundary
- move to `sleep` when memory consolidation is due and no higher-value active engineering work is queued
- if no concrete task is queued but active goals still exist, prefer `ponder` or `manager` rather than idling

### Soft anti-patterns
- stopping after one finished state even though the next state is clear and safe
- repeated `implementation` without review
- repeated `review` without a decision
- repeated `inspection_and_ideation` without narrowing the target
- repeated `planning` on the same work unit without new external information or a real freeze/user-decision branch
- repeated state-shaped activity that does not materially advance, de-risk, decide, freeze, or reprioritize the work
- using `manager` as performative process theater with no priority decisions
- using `cleanup_and_refactoring` as disguised feature work or disguised architectural surgery
- using `refactoring` as a vague beautification spiral
- using `release` to sneak in new logic

### Hard rule
If the heartbeat is no longer sure what state it is in, fall back to `planning` or `ponder`.
If `planning` already produced a concrete owner/file/function seam plus acceptance, the next state must not be `planning` again unless new external information arrived, a binary user decision is needed, or the work is being explicitly frozen.

## State persistence
Store runtime state in `memory/heartbeat_state.json`.

Suggested schema:

```json
{
  "enabled": false,
  "mode": "active",
  "current_state": null,
  "next_state": null,
  "target": null,
  "acceptance": null,
  "task_ref": null,
  "last_result": null,
  "last_ponder_at": null,
  "last_ponder_summary": null,
  "last_manager_at": null,
  "last_sprint_plan_at": null,
  "sprint_due_at": null,
  "updated_at": null
}
```

### Semantics
- `enabled`: master switch
- `mode`: coarse runtime mode (`active` or disabled/inactive usage chosen by the caller)
- `current_state`: state executed in this heartbeat
- `next_state`: queued next state
- `target`: worker-state field for the exact current work unit, may be null/omitted for `manager`, `ponder`, `sleep`, and other non-worker states
- `acceptance`: worker-state field for the measurable done condition, may be null/omitted for `manager`, `ponder`, `sleep`, and other non-worker states
- `task_ref`: optional pointer into a task/issue/doc
- `last_result`: tiny status summary
- `last_ponder_at`: timestamp of the most recent `ponder` pass
- `last_ponder_summary`: tiny summary from the most recent `ponder`
- `last_manager_at`: timestamp of the most recent `manager` pass
- `last_sprint_plan_at`: timestamp of the most recent sprint planning pass
- `sprint_due_at`: due date/time for the next sprint planning or sprint review checkpoint
- `updated_at`: last write time for the state file

## Hard stop rules
Stop and hand off to `planning`, `manager`, or `ponder` if any of these is true:
1. Multiple failed implementation attempts would be needed
2. The work clearly needs architectural redesign
3. The work touches multiple layers unexpectedly
4. Validation failure is global, not local
5. The next sensible action is no longer obvious
6. The task is turning into a long exploratory loop
7. The task starts producing many temporary artifacts without closure

## Non-substantive cycle rule (global)
If two consecutive heartbeats on the same work unit fail to produce material progress, the next heartbeat must not continue the same local loop.
It must do exactly one of:
- execute a bounded change,
- release/cleanup accepted work,
- ask the user for a binary decision,
- freeze the work explicitly,
- or switch to `manager` for reprioritization.

A work unit may not remain in an "active but not really moving" state.
Every active work unit must be in one of these honest statuses:
- advancing,
- blocked on user,
- frozen,
- complete.

## Message contract
Every active heartbeat reply should include:
- `STATE`
- `CHANGED`
- `VALIDATION`
- `RESULT`
- `NEXT_STATE`
- `BLOCKER` (if any)

`TARGET` is optional when it genuinely helps.
It must not appear in `manager` replies.
It may appear in `ponder` replies only when the reflection itself naturally discovered a concrete next focus, not because one was pre-assigned.

If heartbeat is disabled:
- do not emit an idle sentinel reply
- stay quiet or handle the disablement through state/config only
If heartbeat is enabled:
- never reply `HEARTBEAT_OK`
- never treat lack of a pre-queued worker task as permission to idle
If no concrete task is queued but active goals still exist:
- do not idle; prefer `ponder`, `manager`, `inspection_and_ideation`, `planning`, `cleanup_and_refactoring`, or an explicit freeze/handoff

## Repo note
For this repo, heartbeat is for bounded maintenance / planning / small verified improvements.
It must not become the place where policy research runs for hours.
It also must not hide behind an idle state while meaningful bounded work still exists.
For this repo, any heartbeat reply of `HEARTBEAT_OK` is a contract violation.
