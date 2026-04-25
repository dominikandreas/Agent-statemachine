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

## Onboarding and re-onboarding
This repo intentionally does not ship a default `memory/heartbeat_state.json`.

If the workspace is new, or the old long-term goals are obsolete:
1. copy `BOOTSTRAP.example.md` to `BOOTSTRAP.md`
2. let the agent follow it once
3. have the agent ask for high-level and long-term goals
4. write durable goals to `GOALS.md` or `MEMORY.md`
5. seed `memory/heartbeat_state.json` with `next_state: "manager"`
6. delete `BOOTSTRAP.md` when onboarding is complete

That keeps onboarding logic out of normal runtime context.

## Quick start with a custom OpenClaw agent

1. Use this repo as the workspace for your agent.
2. Keep the runtime files small and relevant for your setup:
   - `SOUL.md` for tone/style
   - `USER.md` for operator preferences
   - `AGENTS.md` for workspace rules
   - `HEARTBEAT.md` for runtime and heartbeat behavior
   - `states/*.md` for the actual state definitions
3. In your agent config, point the agent's `workspace` at this repo.
4. Let the agent load `AGENTS.md`, `HEARTBEAT.md`, and only the currently relevant state file during execution.
5. If you use heartbeat memory, keep runtime state in `memory/heartbeat_state.json`.
6. If you want periodic structural hygiene, track `last_refactor_at`, `last_refactor_summary`, and optionally `work_units_since_refactor` in that state file.

Example shape:

```json5
{
  agents: {
    list: [
      {
        id: "main",
        default: true,
        workspace: "/path/to/Agent-statemachine"
      }
    ]
  }
}
```

## Quick start for heartbeat

Minimal OpenClaw heartbeat config:

```json5
{
  agents: {
    defaults: {
      heartbeat: {
        every: "30m",
        target: "last",
        lightContext: true
      }
    }
  }
}
```

Recommended with this scaffold:
- keep `HEARTBEAT.md` present in the workspace
- use `lightContext: true` if heartbeat runs only need `HEARTBEAT.md`
- add `activeHours` if you do not want night-time wakeups
- use `target: "last"` if heartbeat messages should go to the last contact, or `target: "none"` if they should stay internal
- if the repo uses heartbeat memory, let `review` and `refactoring` update `last_refactor_at`, `last_refactor_summary`, and optionally `work_units_since_refactor`

Important note:
- OpenClaw's default heartbeat prompt expects `HEARTBEAT_OK` when nothing needs attention
- this scaffold intentionally avoids idle heartbeat behavior
- if you use stock OpenClaw heartbeat defaults, either relax that rule in `HEARTBEAT.md` or set a custom `heartbeat.prompt` that matches your preferred behavior

Example with an explicit custom heartbeat prompt:

```json5
{
  agents: {
    defaults: {
      heartbeat: {
        every: "30m",
        target: "last",
        lightContext: true,
        prompt: "Read HEARTBEAT.md if it exists (workspace context). Follow it strictly. Use the defined states. Prefer useful bounded work over idle acknowledgements."
      }
    }
  }
}
```

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
- `BOOTSTRAP.example.md` for one-shot onboarding or re-onboarding

## OpenClaw docs
- Heartbeat guide: https://docs.openclaw.ai/gateway/heartbeat
- Gateway configuration: https://docs.openclaw.ai/gateway/configuration
- Local docs mirror inside OpenClaw: `docs/gateway/heartbeat.md` and `docs/gateway/configuration.md`

## Publishing notes
Before publishing or sharing:
- remove private names, hosts, paths, tokens, and infrastructure details
- replace symlinks with regular files if you want portability
- keep non-runtime audit docs out of the execution path
