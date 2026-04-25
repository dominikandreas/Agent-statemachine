# implementation

Perform one bounded engineering change.

## Intent
- execute one concrete unit of work
- think before coding so hidden confusion, inconsistent assumptions, and missed tradeoffs get surfaced before patching
- keep the change narrow and reversible
- prefer the simplest shape that solves the problem without bloating abstractions
- avoid getting trapped in uninterrupted coding momentum
- follow test-driven and best-practice-oriented implementation discipline

## Allowed actions
- edit code, docs, or config
- move files if directly required by the planned change
- add or update tests
- run one bounded validation sequence

## Not allowed
- a second unrelated fix in the same heartbeat
- architecture rewrite without a prior planning state
- repeated speculative patch loops
- shipping a new feature without a test
- broad "while I am here" cleanup that changes the scope

## Implementation rules
- Prefer test-driven development when practical.
- Every new feature requires at least one test.
- Behavior changes must have corresponding test coverage.
- Before editing, check for confusion, inconsistent assumptions, or unresolved tradeoffs. If they matter, surface them instead of coding past them.
- Simplicity first: do not introduce bloated abstractions, oversized constructions, or architectural ceremony when a smaller clear solution would do.
- Make surgical changes: avoid touching orthogonal code, comments, or structure you do not need for the bounded work unit.
- Keep correct layer ownership, avoid duplicate logic, prefer clear interfaces, and keep changes small and reviewable.
- The work unit must stay singular:
  - one primary target
  - one primary validation command or sequence
  - at most one tiny immediate corrective follow-up for a trivial integration breakage

## Budget
- one coherent change set
- one validation pass
- optionally one tiny immediate corrective follow-up for a trivial breakage revealed by that validation

## Required outputs
- exact files changed
- exact command(s) run
- pass or fail result
- if no file changed, provide concrete execution evidence such as test or log output, or an explicit freeze or user-decision path

## Enforcement (explicit)
- If no real blocker exists, implementation must include at least one execution step that moves the work.
- No-op implementation replies without blocker are invalid.
- After one no-op miss, the next implementation wake must do exactly one of:
  1. execute the seam,
  2. explicitly freeze or hand off,
  3. ask one binary user decision.
- Pre-reply self-check: "Did I run a tool that moved the work?" If no, do not finalize the heartbeat yet.

## Typical next states
- `review` if implementation landed
- `refactoring` if the change exposed one clear structural seam that should be simplified before more feature growth
- `planning` if blocked or scope was wrong

## Stop immediately if
- the first validation shows conceptual failure rather than syntax or integration failure
- more than one fix attempt would be needed
- the change spills into multiple unrelated areas
- the planned work unit was actually too vague or too broad
