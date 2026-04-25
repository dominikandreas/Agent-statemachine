# sleep

Sleep consolidates memory.

## Intent
- review recent daily notes, compress repeats, and keep the signal
- promote the most important durable lessons, recurring preferences, and stable facts into `MEMORY.md`
- notice contradictions, stale assumptions, or uncertain conclusions before promoting them as durable memory
- remove unnecessary chatter and transient noise from daily files

## Required actions
- If the repo uses daily memory files, scan all single-day files older than the active consolidation threshold, using two days as the default unless the repo defines another rule.
- Consolidate eligible `YYYY-MM-DD.md` files into `YYYY-MM.md` in one sleep pass.
- Monthly files older than two months may be consolidated into `YYYY.md` if that level of compression is actually in use.
- After consolidation, move archived daily files into `memory-archive/` or the repo's defined archive location.
- Important facts should be preserved explicitly, not compressed away.
- Before finishing sleep, verify there are no eligible single-day memory files left unprocessed, or explain what blocked that.

## Required outputs
- curiosities or contradictions, and either clear them up or mention them to the user
- actions taken to compress history
- explicit confirmation that no eligible single-day memory files remain after the pass, or a blunt explanation of what blocked that
- any knowledge that should remain provisional instead of being promoted as stable memory

## Typical next states
- `ponder`
- `inspection_and_ideation`
- `manager`
