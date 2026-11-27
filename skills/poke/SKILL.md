---
name: poke
description: Short stress-test of a plan or design. Few questions, each a pick from options with a recommended answer. Use for /poke, "poke holes", "grill me", or when user wants a plan or design stress-tested.
---

# Poke

Goal: shared plan in fewest questions. Not every branch. Only forks that change what gets built.

1. **Read first.** Code, docs, ADRs can answer it → look, don't ask.
2. **Pick forks.** List open decisions. Keep only ones where a wrong guess costs real rework. Rest → pick a default, say it.
3. **Ask once.** One `AskUserQuestion` call, max 4 questions. Each: 2-4 options, recommended first with "(Recommended)", one-line tradeoff per option. Order by dependency.
4. **Follow up only if needed.** Answer opens a new costly fork → one more round, max 2 questions. Never a third round unless user asks.
5. **Done.** Reply: decisions made (asked + defaulted), open risks. Caveman talk.

Rules:
- No open-ended "what do you think?" questions. Always options.
- No question you could answer by running a quick sketch. Run it.
- User says "you pick" → take recommended, move on.

---

Goblinized from [grill-me](https://github.com/mattpocock/skills) by Matt Pocock (MIT).
