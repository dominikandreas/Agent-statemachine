# review

Check what changed and whether it is actually acceptable.

## Intent
- verify correctness
- enforce best software engineering practices
- catch drift, leftovers, dead code, or broken contracts

## Allowed actions
- run tests / checks
- inspect diffs / status
- inspect docs consistency
- inspect artifact hygiene
- inspect whether legacy / new boundaries were violated
- produce review notes / follow-up tasks

## Not allowed
- broad new implementation work
- opportunistic feature additions

## Required outputs
- `VERDICT`: pass / pass-with-followup / fail
- exact findings

## Typical next states
- `release` if acceptable
- `implementation` if one small fix is clearly defined
- `refactoring` if the behavior is acceptable but the code shape should be simplified before more growth piles on
- `planning` if the problem is broader than one small fix

## Review checklist
- do all relevant tests pass?
- if a new feature was added, does it have a test?
- are tests still aligned with the intended behavior?
- does code live in the correct layer / package?
- is a refactor warranted before more work piles onto the current shape?
- are docs up to date?
- did we create junk artifacts / dead paths?
- did we accidentally touch legacy runtime when active runtime should own it?
- did the review verdict get applied to the correct work unit and recorded in the correct memory/state files?

## Correction rule
- If you realize the review was attached to the wrong work unit, wrong state, or wrong recorded conclusion, fix the affected memory/state files immediately in the same turn before replying.
- Do not ask whether to correct obvious review bookkeeping mistakes. Just correct them, then report the corrected verdict.
