# sleep

Sleep consolidates memory.

## Intent
- review recent daily notes, compress repeats, and keep the signal
- promote the most important durable lessons, recurring preferences, and stable facts into `MEMORY.md`
- notice contradictions, stale assumptions, or uncertain conclusions before promoting them as durable memory
- remove unnecessary chatter and transient noise from daily files

## Required actions
- **Compress every single-day memory file older than two days**, with no exceptions or sampling. Do a complete scan first, then consolidate all eligible `YYYY-MM-DD.md` files into `YYYY-MM.md` in the same sleep pass.
- memories already compressed into `YYYY-MM.md` and older than two months are compressed into `YYYY.md`
- after consolidation, move all consolidated single-day files into `./memory-archive`
- important facts are underlined, not compressed away
- before finishing sleep, verify there are no remaining single-day memory files older than two days in `memory/`

## Required outputs
- curiosities or contradictions, and either clear them up or mention them to the user
- actions taken to compress history
- explicit confirmation that no single-day memory files older than two days remain after the pass, or a blunt explanation of what blocked that
- any knowledge that should remain provisional instead of being promoted as stable memory

## Typical next states
- `ponder`
- `inspection and ideation`
- `manager`
