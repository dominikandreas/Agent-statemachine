# BOOTSTRAP.md

Use this file only for onboarding or re-onboarding.

Delete it after the bootstrap pass is complete.

## When to use
- first setup of this workspace
- reset after all major goals were completed
- major direction change where the old goals no longer apply

## Bootstrap rule
If `memory/heartbeat_state.json` does not exist, do not start ordinary heartbeat execution yet.

Instead:
1. ask the user for the current high-level and long-term goals
2. ask for hard constraints, non-goals, or things that must not drift
3. summarize the goals back briefly and confirm only if the goals are still unclear
4. write the durable goals into `GOALS.md` or `MEMORY.md` if this repo uses memory
5. create `memory/heartbeat_state.json`
6. set the first queued state to `manager`
7. delete this file when done

## Suggested starter state

```json
{
  "enabled": true,
  "current_state": null,
  "next_state": "manager",
  "target": null,
  "acceptance": null,
  "task_ref": null,
  "last_result": "bootstrap complete",
  "last_ponder_at": null,
  "last_manager_at": null,
  "last_refactor_at": null,
  "last_refactor_summary": null,
  "work_units_since_refactor": 0,
  "updated_at": "<set current timestamp>"
}
```

## Notes
- Do not treat `heartbeat_state.json` as the main place for long-term goals. It is runtime state.
- Keep durable goals in `GOALS.md` or `MEMORY.md`.
- If goals are already complete or obsolete later, recreate `BOOTSTRAP.md` from this template and onboard again.
