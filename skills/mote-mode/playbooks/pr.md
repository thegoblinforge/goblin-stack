# PR

1. Branch off main (worktree if parallel work exists). Never commit unrelated changes.
2. Small ordered commits; each could land alone. Amend when fix belongs in last commit.
3. `review` skill over diff.
4. Title: Conventional Commits `type(scope): subject`, imperative, no period.
5. Body is a one-minute briefing for someone with the diff. `##` sections, drop empty ones:
   - `## Why` 1-3 sentences.
   - `## What changed` 1-3 bullets.
   - `## Scope` covers / leaves out.
   - `## Tradeoffs` only rejected alternatives a reviewer would ask about.
   - `## Verification` real run paths + outcome (from `verify`).
6. Write body with plain verbs, articles kept, one word per action; then `unslop`.
7. `gh pr create` (ready, not draft). Post URL. Don't babysit unless asked.
