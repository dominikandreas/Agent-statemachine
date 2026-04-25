# Agent State Machine

A lightweight scaffold for running bounded agent work through explicit states instead of vague autonomous loops.

## Runtime files
These are the files that matter during execution:
- `SOUL.md`
- `USER.md`
- `TOOLS.md` when relevant
- `AGENTS.md`
- `HEARTBEAT.md`
- one active state file from `states/`
- `memory/heartbeat_state.json` only if the repo uses heartbeat memory

Everything else is reference material.

## States
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

## Suggested flow
A common flow is:
1. `ponder` or `manager`
2. `planning`
3. `implementation`
4. `review`
5. `release`

Use `cleanup` for standalone hygiene work.
Use `refactoring` when the right next move is structural simplification rather than feature work.

## Top-level templates
These are templates, not mandatory standards:
- `SOUL.md` for style or persona
- `USER.md` for operator preferences
- `TOOLS.md` for local commands or notes
- `AGENTS.md` for workspace rules
- `HEARTBEAT.md` for runtime behavior

## Publishing notes
Before publishing or sharing:
- remove private names, hosts, paths, tokens, and infrastructure details
- replace symlinks with regular files if you want portability
- keep non-runtime audit docs out of the execution path
