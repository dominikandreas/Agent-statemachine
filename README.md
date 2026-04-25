# Agent State Machine

A lightweight workspace scaffold for running bounded agent work through explicit states instead of vague autonomous loops.

## What this repo contains

- `AGENTS.md` - workspace operating rules
- `SOUL.md` - persona and working style template
- `USER.md` - operator preferences template
- `TOOLS.md` - repo-local notes and useful commands
- `HEARTBEAT.md` - heartbeat runtime guidance
- `states/` - state definitions and the state machine overview

## Core idea

The agent should always operate from one clear primary state at a time.
Typical states include:

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

A state can transition to another state when the next step is obvious, safe, and bounded.

## Suggested usage

1. Copy this workspace scaffold into a fresh repo or workspace.
2. Adjust the top-level files for your environment. These are templates, not mandatory standards:
   - `SOUL.md` for persona/style
   - `USER.md` for operator preferences
   - `TOOLS.md` for local commands and non-secret notes
   - `AGENTS.md` for workspace-specific rules
   - `HEARTBEAT.md` if you use heartbeat-driven execution
3. Keep the `states/` directory as the main state definition layer.
4. If you use memory files, store runtime continuity in `memory/heartbeat_state.json` and daily notes in `memory/YYYY-MM-DD.md`.
5. Run work in small bounded loops: plan, implement, review, release.

## Minimal workflow

A common flow looks like this:

1. `ponder` or `manager` to orient
2. `planning` to define one concrete target
3. `implementation` to make one bounded change
4. `review` to verify it
5. `release` to clean up and publish

If the task is too vague, go back to `planning`.
If the task turns into structural simplification, switch to `refactoring`.
If no concrete implementation seam exists, use `inspection_and_ideation` or `ponder`.
If the repo needs hygiene work outside a specific shipping step, use `cleanup`.

## Customization notes

Before publishing or sharing:

- remove private names, hosts, paths, tokens, and infrastructure details
- replace any symlinks with regular files if you want the repo to be portable
- make sure `USER.md`, `TOOLS.md`, and `AGENTS.md` match the intended public or private use
- check that any memory examples or local notes do not point to a private local path
