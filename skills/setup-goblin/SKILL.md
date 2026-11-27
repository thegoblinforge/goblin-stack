---
name: setup-goblin
description: Configure which models goblin-stack subagents use per role, cheapest first, low to medium effort. Writes ~/.claude/rules/goblin-models.md. Use for /setup-goblin or "configure goblin models".
disable-model-invocation: true
---

# Setup goblin

Write `~/.claude/rules/goblin-models.md`. Claude Code loads every file in `~/.claude/rules/` into new sessions, so role lines are in context without a read.

Policy: cheapest model that can do the role, effort `low` or `medium` only. Stronger models are an escalation step, not a default, because most subagent work is reading and mechanical edits.

## Steps

1. **Detect.** Available models = `model` enum in the `Agent` tool schema (e.g. `haiku`, `sonnet`, `opus`, `fable`). Efforts = its `effort` enum, limited to `low` and `medium`. Never write a model not detected.
2. **Load.** File exists → read it, keep user's custom lines. Drop roles not in step 3.
3. **Build table** (cheapest detected model per tier):

   | Role | Default |
   | --- | --- |
   | explore (bulk reads, search) | haiku low |
   | how explorer | haiku low |
   | edits (mechanical, scoped) | sonnet low |
   | review and prose | sonnet low |
   | interrogate reviewers | sonnet low, haiku low |
   | hardest tasks (cross-cutting design, concurrency) | sonnet medium |
   | escalation | opus medium |

   A tier's model missing → next cheapest detected model, same effort.
4. **Confirm.** Show the table and the file diff. Ask with `AskUserQuestion`: accept, or change specific roles (detected models + `inherit-parent`). This writes persistent config, so wait for a yes.
5. **Write.** Overwrite whole file (idempotent), no frontmatter:

```
# goblin-stack model configuration. One line per role. Delete a line to use the skill default.
# inherit-parent: role runs on the parent chat model (omit Agent model).
# Escalation: start at the role's line. Move up one step (low → medium, then haiku → sonnet → opus)
# only after a failed attempt or for a named hardest task, and say why in the reply. Never above medium effort.
explore: haiku low
how explorer: haiku low
edits: sonnet low
review and prose: sonnet low
interrogate reviewers: sonnet low, haiku low
hardest tasks: sonnet medium
escalation: opus medium
```

6. **Done.** Tell user the rule applies to new sessions; rerun to change.
