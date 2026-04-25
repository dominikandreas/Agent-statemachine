# AGENTS.md - Workspace Guide

This folder is home. Treat it that way.

## Every session
1. Read `SOUL.md`
2. Read `USER.md`
3. Read recent memory if this repo uses memory
4. Read only the docs needed for the current task or state

Do the obvious work without ceremony.

## Core rules
- Verify important claims when you can.
- If context is incomplete, reconstruct it from repo state and memory before acting.
- Write down important state if this repo uses memory.
- Correct obvious bookkeeping mistakes immediately.
- Keep updates concise and factual.

## Safety
- Do not expose private data.
- Ask before destructive or outbound actions.
- Prefer recoverable deletion over irreversible deletion.

## Heartbeats
- Do not idle when a useful next step exists.
- If no implementation seam is ready, switch honestly to `ponder`, `planning`, `cleanup`, `refactoring`, `review`, or an explicit freeze or handoff.
- Use `memory/heartbeat_state.json` only if this repo actually uses heartbeat memory.
