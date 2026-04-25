# sleep

Consolidate memory.

## Intent
- compress old notes without losing durable signal
- promote stable facts into `MEMORY.md` when the repo uses it
- reduce noise before it hardens into fake memory

## Required actions
- if the repo uses daily memory files, consolidate eligible `YYYY-MM-DD.md` files into `YYYY-MM.md`
- if the repo also uses monthly rollups, consolidate older `YYYY-MM.md` files into `YYYY.md`
- move processed daily files into the archive location the repo uses
- preserve important facts explicitly instead of compressing them away
- report contradictions or uncertainty instead of promoting them as stable truth
- verify that no eligible daily files remain unprocessed, or explain what blocked that

## Required output
- what was consolidated
- whether anything was blocked
- what should remain provisional

## Typical next states
- `ponder`
- `inspection_and_ideation`
- `manager`
