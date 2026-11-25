---
name: how
description: Explain how code works at a senior-onboarding level, before changing it or to answer "how does X work", "where should this live", "which module owns this", "is this the right layer". Use for code walkthroughs, runtime flow, and placement questions.
---

# How

Goal: working mental model of a subsystem, not annotated source.

1. Scope. Ambiguous → state your reading and go; user can redirect.
2. Explore inline: `rg` for entry points, read the key files, trace one real call path end to end.
3. Wide scope only (many dirs or services, would flood context) → one `Explore` agent, model per `how explorer` line in `~/.claude/rules/mote-models.md` (default `haiku` low). Brief: question, dirs, "return file:line refs + 1-line role each, no file dumps". Never more than one.
4. Write answer yourself.

## Output

Drop sections that don't apply:
- **Overview.** 2-3 sentences: what it does, for whom.
- **Key concepts.** Core types/data shapes and what they mean.
- **How it works.** Main flow as numbered steps with `file:line`.
- **Where things live.** Path → responsibility.
- **Gotchas.** Surprises, invariants, traps.

Placement question → add a recommendation with the reason.
