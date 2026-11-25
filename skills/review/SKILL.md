---
name: review
description: Pre-commit cleanup pass over the current diff. Removes slop code (needless guards, one-caller wrappers, dead paths, debug leftovers) and comments that don't earn their place. Use before any commit or PR, or when asked to deslop, clean up the diff, or strip comments.
---

# Review

Inline pass by you. No subagent; you already hold the context.

## Scope

Caller's files or diff. Default: `git diff main...HEAD` plus working tree.

## Code slop: fix directly

- Guards, try/catch, null checks for states that can't happen inside typed code (Boundary Discipline).
- One-caller wrappers, single-impl adapters, speculative params or options.
- Dead branches, unused imports, commented-out code, debug logs.
- Duplicated decision → one source of truth.
- Style inconsistent with surrounding file.

## Comments: delete by default

Keep only:
- License/legal headers.
- Non-obvious behavior forced by something we can't change (dependency, platform, vendor, protocol).
- Public API doc comments that define a contract.
- Issue/RFC link explaining a constraint code can't express.
- Formatter/lint pragmas whose rule is wrong or style-only.

Everything else goes: narration, banners, restated code, "IMPORTANT / do not remove / fine for now" without proof.
A surprise in *our* code → delete the comment and fix the code so it's obvious (rename, extract, type). Too big for scope → report it as open.
Suppressions (`@ts-ignore`, `eslint-disable`, `# type: ignore`) guarding a real-bug rule → remove and fix the cause.

## Then

Rerun the project check (tests/lint/typecheck) once. Report: files touched, comments deleted, code fixes, open items. Plain sentences.
