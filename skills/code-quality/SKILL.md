---
name: code-quality
description: Generic layered architecture (route, service, repository), code smells and safe refactoring. Use when designing, writing, reviewing or refactoring code, or when asked about code smells, layers or best practices.
---

# Code quality

Project rules and ADRs win over this file.

## Layers

Calls go down only: route → service → repository.

| Layer | Owns | Hands off |
| --- | --- | --- |
| Route (HTTP, RPC, job, queue) | auth, input validation, one service call, response mapping | rules and queries |
| Service | rules, orchestration, ownership checks, a result union | transport objects |
| Repository | queries for one concept, returning domain data | decisions |

- Two routes with the same steps share one service function. Keep real differences as arguments.
- An atomic guard (cap, claim, state transition) lives in the write statement; the service names it.
- **Deletion test** decides a repository: delete it; if no complexity returns to callers, the service queries directly.

## Write

- One rule, one **owner**. A second copy of a predicate, default or sequence moves to the owner, with every caller.
- Union with `kind` or `ok` over optional fields and thrown control flow.
- Pass in clock, network and model, so tests run real code through the interface.
- Split a module by reason to change.
- A rule a regex can spot gets a test that fails on a second copy.

## Refactor

1. Record a green baseline and pass count. Untested behaviour gets a test first.
2. Bug found: failing test, fix, own commit, before moving code.
3. Move in small units, each green and committed. Behaviour stays the same; a change to it is a product decision: ask.
4. Migrate every caller and delete the old name, no shim. Done when a repo-wide search finds none.
5. A removed test gets a replacement on the production path, or a line in the report.

## Review

Check each changed file against **Layers**, **Write** and every group in [`smells.md`](smells.md).

Finding = `file:line`, name, the change it makes costly, the move. A smell is a lead: report it only with that cost. Done when every file has findings or "none".
