---
name: tinker
description: Find the few refactors that make a codebase easier to change and test, using code-quality rules plus module depth. Use for /tinker, "improve the architecture", "what should we refactor", or making code more testable and AI-navigable.
disable-model-invocation: true
---

# Tinker

Rules come from `../code-quality/SKILL.md` (layers, one owner per rule, refactor steps) and its `smells.md`. This skill adds **depth** and a short loop.

## Depth

- **Module** = anything with interface + implementation (function, class, package).
- **Interface** = all a caller must know: types, invariants, order, error modes, config.
- **Deep** = much behaviour behind small interface. **Shallow** = interface about as big as body. Want deep.
- **Deletion test**: delete it. Complexity vanish → pass-through, inline it. Complexity spread to N callers → keeps its place.
- **Interface is test surface.** Test needs to reach past it → wrong shape.
- **One adapter = fake seam, two = real.** No port without prod + test adapter.
- **Replace, don't layer.** Tests at new deep interface replace old shallow-module tests; delete those.

## Loop

1. **Read.** `CONTEXT.md` and `docs/adr/` if present. ADRs are settled; reopen only if friction is real, and say so.
2. **Explore inline.** Narrow to user's area if given. Wide repo → one `Explore` agent (haiku low), brief: "file:line + one-line friction each". Look for:
   - one concept spread over many tiny modules,
   - shallow modules and pass-throughs (deletion test),
   - code-quality smells with a real change cost (Shotgun Surgery, Feature Envy, Middle Man, layer leaks),
   - code hard to test through its interface.
3. **Rank.** Keep top 3 by cost of change today. Drop theory.
4. **Present.** Numbered, each: files, problem, move, gain (locality, leverage, tests). Use domain names from `CONTEXT.md`. No interface designs yet.
5. **Pick.** `AskUserQuestion`: which candidate (or none). Recommended first.
6. **Shape.** Run `../poke/SKILL.md` on the chosen one. Novel interface → sketch 2 signatures inline, recommend one. No parallel design agents.
7. **Record.** User rejects for a lasting reason → offer one ADR line so it isn't re-suggested. New domain term → add to `CONTEXT.md`.

Doing the refactor → `refactoring` playbook and code-quality Refactor steps.

---

Depth vocabulary goblinized from [improve-codebase-architecture](https://github.com/mattpocock/skills) by Matt Pocock (MIT).
