# mote-stack

A token-light fork of [pstack](https://github.com/cursor/plugins/tree/main/pstack) by Lauren Tan (MIT). Mote is cheap Chilean husked wheat. It costs less than a poteto.

mote-stack keeps pstack's engineering principles and its writing rules. It cuts most of the process that spends tokens without changing the result.

## Who it's for

mote-stack is for people on a budgeted subscription, such as Claude Pro, who hit usage limits and want every token to count. In Chilean Spanish, it helps you "exprimir el jugo": squeeze the juice out of your plan. If you have a large plan or pay per token without a cap, pstack's heavier process may be worth its cost to you.

## Install

```bash
claude plugin marketplace add thegoblinforge/mote-stack
claude plugin install mote-stack@mote-stack-local
```

From a local clone, pass the folder path to `marketplace add` instead.

Then in a session, type `/mote-stack:mote-mode`. Run `/mote-stack:setup-mote` once to pick models.

## What it contains

| Skill | Use |
| --- | --- |
| `mote-mode` | The working style. Principles index, autonomy rules, reply rules, and a router to five playbooks (feature, bug fix, refactoring, investigation, PR). |
| `unslop` | Removes AI writing patterns. Ported from pstack with its rule numbers. |
| `review` | Pre-commit pass over the diff for slop code and useless comments. Runs inline. |
| `verify` | Minimal proof that a change works: one positive and one negative scenario, run on the real artifact. |
| `how` | Explains how code works. Inline by default, at most one explorer for wide scopes. |
| `figure-it-out` | Designs a bespoke plan for large or cross-cutting work. |
| `interrogate` | Adversarial review by at most two reviewers. Only runs when you ask. |
| `setup-mote` | Writes `~/.claude/rules/mote-models.md`. Cheapest model first, low or medium effort. |

The `mote-agent` subagent handles scoped edits. Its rules live in its own file, so it never reads the main skill.

## What was cut, and why

pstack loads about 26KB before any work: the 20KB `poteto-mode` skill plus a Cursor-to-Claude adapter. Each cited principle requires reading its own file. Features must go to a delegate or a multi-model arena, `how` spawns up to five agents, and default models run at xhigh effort. mote-stack changes these points.

- The main skill is under 6KB and uses Claude Code tool names, so there is no adapter.
- All 22 principles sit in one reference file, read only when the one-line index is not enough.
- Work runs inline. Automatic fan-out stops at two agents, used for bulk reads or isolated edits.
- Model choice starts at haiku or sonnet with low or medium effort, and moves up one step only with a stated reason.
- Playbook steps go into the task list in short form. There is no verbatim copy, throughput checkpoint, or decision-log file.

Dropped skills: arena, swarm, architect (now one line about sketching types first), reflect, why, orchestrate, autopilot-full, autopilot-stack, autonomous run, overnight, hillclimb, runtime and trace forensics, statechart, the four verification-skill generators (replaced by `verify`), ketchup, ketchup-video, recall, teach, sharpen, bro, automate-me, make-bot-ui, show-me-your-work, poteto-help, typescript-best-practices, benchmark-checklist (now one principle line), and the bundled scripts (watch-pr, orch, check-plan).

To bring one back, copy it from pstack and remove its mandatory fan-out.

## Measured cost

Tested 2026-11-25 on a small Python CLI fixture. There were 3 tasks (bug fix, feature, "how does it work"), one run each per plugin. Every run used `claude-sonnet-5-5` at medium effort. Costs are measured token counts multiplied by list prices. The cache-write price is assumed at 1.25 times input.

| Model | Input $/M | Cache write $/M | Cache read $/M | Output $/M |
| --- | --- | --- | --- | --- |
| Haiku 5.5 | 0.10 | 0.125 | 0.01 | 0.50 |
| Sonnet 5.5 | 2.00 | 2.50 | 0.10 | 10.00 |
| Opus 5.5 | 4.00 | 5.00 | 0.20 | 20.00 |

| Task | mote-stack | pstack |
| --- | --- | --- |
| Bug fix | $0.238 | $0.253 |
| Feature | $0.191 | $0.301 |
| How it works | $0.231 | $0.307 |
| **Total on Sonnet 5.5** | **$0.66** | **$0.86** |
| Same tokens priced on Haiku 5.5 | $0.039 | $0.050 |
| Same tokens priced on Opus 5.5 | $1.32 | $1.72 |

Both plugins passed all 12 checks. mote-stack cost 23% less and ran about 25% faster.

- Most of each run's cost is the cache write for about 70-80K tokens of fixed system and tool context. Skill text is a small share of that.
- The mote feature run likely hit an already warm cache. With the earlier feature run instead, the saving is 17%.
- The baseline favors pstack. Its default models (opus at xhigh) and its required helper agents did not run on these small tasks.
