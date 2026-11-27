# Refactoring

Structure changes. Behavior doesn't. Found a real bug or missing feature → split it out, ship structure first. Follow `code-quality` (Refactor steps, smells as leads) alongside these steps.

1. Pin behavior first: characterization test, snapshot, or old-vs-new output diff. Type check and lint are not a pin.
2. Name target shape as if built today. It must delete branches or invalid states, not add indirection.
3. Subtract first: dead code, one-caller wrappers, redundant validators, orphan refs.
4. Move in small steps, pin green after each. API reshape → migrate all callers and delete old API same wave, no shims. Grep renames in strings and docs too. Large mechanical edits → one `mote-agent` or a codemod (Build the Lever).
5. Prove pin still passes on real artifact.
6. Keep only if reader load dropped. Otherwise revert.
7. Commits: subtraction, then reshape. `pr`.

**Reply:** structure changed, pin used, equivalence proof, reader-load change, what was reverted.
