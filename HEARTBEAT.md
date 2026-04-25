# HEARTBEAT.md

Heartbeat is for useful bounded work, not an open-ended autonomous loop.

## Load order
1. Read `TOOLS.md` if relevant.
2. Read this file.
3. Read `memory/heartbeat_state.json` if this repo uses heartbeat memory.
4. Read the current state file in `states/`.

## Available states
- `ponder`
- `manager`
- `inspection_and_ideation`
- `planning`
- `implementation`
- `review`
- `release`
- `cleanup`
- `refactoring`
- `sleep`

## Core rules
- Operate from one primary state at a time.
- A single heartbeat may execute multiple sequential states if the next step is obvious, safe, and bounded.
- Every heartbeat must achieve at least one meaningful outcome: progress, uncertainty reduction, a required decision, an honest freeze or close, or priority steering.
- If the current state is unclear, fall back to `planning` or `ponder`.
- If no concrete task is queued, do not idle. Prefer `ponder`, `manager`, `cleanup`, or `refactoring`.
- Never reply with an idle sentinel such as `HEARTBEAT_OK`.
- Never use heartbeat as cover for a patch spiral or vague process theater.

## Default transitions
- `ponder` for reflection and drift detection
- `manager` for steering goals and priorities
- `inspection_and_ideation` when the problem is visible but the next move is not
- `planning` when a vague direction needs one bounded work unit
- `implementation` when one bounded change is ready
- `review` after a meaningful change or verification pass
- `release` when accepted work only needs shipping cleanup, docs, or publish steps
- `cleanup` for standalone repo hygiene and leftover classification
- `refactoring` when review or broader repo inspection shows that structural simplification is now the highest-value next move
- `sleep` when memory consolidation is due and no higher-value active work is queued

## Hard stops
Stop and hand off to `planning`, `manager`, or `ponder` if:
- multiple failed implementation attempts would be needed
- the work needs architectural redesign
- the task spills across multiple layers unexpectedly
- validation failure is global rather than local
- the next sensible action is no longer obvious
- the work is turning into open-ended exploration

## Runtime state
If this repo uses heartbeat memory, store runtime state in `memory/heartbeat_state.json`.
Suggested fields: `enabled`, `current_state`, `next_state`, `target`, `acceptance`, `task_ref`, `last_result`, `last_ponder_at`, `last_manager_at`, `last_refactor_at`, `last_refactor_summary`, `work_units_since_refactor`, `sprint_due_at`, `updated_at`.

Refactor tracking guidance:
- `last_refactor_at` records the last completed refactoring pass
- `last_refactor_summary` records what was simplified
- `work_units_since_refactor` is an optional counter for how much accepted work landed after the last refactor
- if refactor tracking is stale, missing, or clearly drifting upward, `review` should check the broader codebase for refactor candidates instead of only reviewing the local diff

## Reply contract
Every active heartbeat reply should include:
- `STATE`
- `CHANGED`
- `VALIDATION`
- `RESULT`
- `NEXT_STATE`
- `BLOCKER` when relevant

`TARGET` is optional when helpful.
- do not emit `TARGET` in `manager`
- `ponder` may emit `TARGET` only if reflection naturally converges on one

## End condition
At the end of an active heartbeat:
- update daily memory if this repo uses memory and it matters
- update `memory/heartbeat_state.json` if this repo uses heartbeat memory and the state changed
- after a completed `refactoring` pass, update `last_refactor_at` and `last_refactor_summary`
- after accepted non-refactor work lands, increment or otherwise refresh `work_units_since_refactor` if this repo tracks it
