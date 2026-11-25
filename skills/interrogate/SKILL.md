---
name: interrogate
description: Adversarial review of a change by up to two independent reviewers. Use only when the user asks for /interrogate, "adversarial review", "challenge this", "tear this apart", or "find blind spots".
disable-model-invocation: true
---

# Interrogate

Explicit-only, because each reviewer re-reads the diff. Deliverable is a verdict. Don't auto-apply changes.

1. **Scope.** User's files/diff, else `git diff main...HEAD`.
2. **Intent.** One paragraph from user message, commits, PR body. Unsure → ask before spawning.
3. **Reviewers.** Default one reviewer. Two only if change is high-stakes (concurrency, security, data loss, public API) or user asks. Models from `interrogate reviewers` line in `~/.claude/rules/mote-models.md`; default `sonnet` low; second reviewer uses a different model (e.g. `haiku` low or `opus` medium) for diversity. Spawn in one message, `subagent_type: general-purpose`, brief says "read-only, do not edit".
4. **Reviewer brief.** Intent + diff path (not pasted) + this rubric:
   - Correctness: does it do the intent? Edge cases, error paths, concurrency.
   - Design: right data shape? Needless layers? Simpler alternative?
   - Blast radius: what else could break beyond the diff?
   - Tests: do they fail if behavior breaks?
   Return findings as: severity (blocker / should / nit), `file:line`, claim, evidence, suggested fix. No praise.
5. **Synthesize yourself.** Check each finding against code. Drop ones you can refute, with reason. Both reviewers agree → high signal.

**Reply:** verdict (ship / fix first / rethink), confirmed findings by severity, dismissed ones with one-line reason.
