---
name: figure-it-out
description: Design a bespoke, auditable plan when no narrow playbook fits, such as a large migration, an ambitious multi-part change, or work a human reviews after stepping away. Scales rigor to stakes and runs a hypothesis loop. Use for /figure-it-out, "figure it out", or big cross-cutting tasks.
---

# Figure it out

Deliverable before code: the workflow itself, a phase list a human can review.

## A. Frame

Before starting, state:
- Done = a falsifiable predicate (what you'll run, what result means pass).
- Scope: rough units, effort, known blockers.
- Rigor level. One-way doors and wide blast radius get more gates. Reversible low-stakes steps get fewer. Rigor = gates and checks, not "try harder".

Show the framing. Reversible work proceeds; a multi-hour run gets one checkpoint with the human first.

## B. Design

- Split into units that each land alone. Riskiest unknown first. Scaffold and checks before features.
- Build the check before the work and capture baseline from pre-change state, so the result reads "old vs new".
- One-way-door design → sketch 2-3 shapes cheaply (types, signatures), pick one, note why. Skip for mechanical work.
- Fan-out: parallelize only across real seams, own branch/worktree each, max 2 agents unless user allows more.
- Write the phase list into the plan file or task list.

## C. Loop

Each unit is an experiment. State hypothesis, smallest change, measure against predicate on real artifact, keep if it advanced, revert if not. Verify each unit before the next.
- Inspect artifacts, never self-reports. Passes too easily → suspect the check.
- Verdict per unit: VERIFIED / NOT VERIFIED / INCONCLUSIVE. Inconclusive ≠ pass.
- Gate is wrong → fix gate in its own change, don't route around it.

## D. Trail

Keep one line per real decision (what, why, evidence) in the plan file. Commit it only if a reviewer needs it.

## E. Hand back

Check the whole against the A predicate on the real product (`verify` skill). Recurring correction → encode as a lint, check, or script.

**Reply:** the plan you designed, rigor level and why, what's verified, what's open.
