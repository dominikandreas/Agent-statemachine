# inspection_and_ideation

Inspect current behavior and generate the next valuable improvement idea.

## Intent
- study current policy / sim behavior when active goals exist but no concrete next step is ready
- identify the next high-value target
- generate bounded ideas rather than blind patches

## Allowed actions
- inspect metrics, traces, artifacts, and failing tests
- compare current behavior vs goal behavior
- identify concrete bad windows / anomalies / regressions
- formulate 1-3 plausible hypotheses or improvement directions
- rank the next target
- write / update a short ideation artifact or task entry

## Not allowed
- endless diagnostics without narrowing the target
- broad coding loops
- turning the state into disguised implementation

## Required outputs
- one concrete observed problem or gap
- one concrete target window / metric / symptom
- 1-3 plausible next ideas or hypotheses
- one prioritized next step

## Typical next states
- `planning`
- `implementation` if the fix is already obvious
