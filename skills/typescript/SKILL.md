---
name: typescript
description: Lightweight TypeScript rules for type-safe code. Use when writing, editing, or reviewing any .ts or .tsx file.
paths: ["**/*.ts", "**/*.tsx"]
---

# TypeScript

Goal: compiler rejects illegal states, so fewer runtime checks and bugs.

- **Unions over optional bags.** Variants get a `kind` literal: `{ kind: "ok"; value: T } | { kind: "err"; error: E }`.
- **Exhaustive switch.** Default arm: `const _x: never = v;` so a new variant fails the build.
- **Brand look-alike primitives.** `type UserId = string & { readonly __brand: "UserId" }`. Create only via a checking guard (`isUserId(x): x is UserId`), never `as`.
- **`unknown`, not `any`,** for external data. Parse once at the boundary into a named type; trust it inside. Repo has zod/valibot → use the schema and `z.infer`, don't hand-write guards.
- **No `as`.** Only right after validation. Prefer `satisfies` to check a literal without widening.
- **Narrow in this order:** discriminant switch > `in` > `typeof`/`instanceof` > type guard > `as`. A guard must actually check what its name claims.
- **Shape makes bad values impossible** where cheap: `[T, ...T[]]` for non-empty. Keep `T[]` until the loose type forces `!` or a cast.
- **Derive types** with `Pick`/`Omit`/`ReturnType`/`Awaited`/`typeof` before writing a new interface.
- **Object args** for 3+ params or same-typed params. Skip on hot paths.
- **Tests run real code;** mock only what can't run locally. No `console.log` in shipped code; use the repo's logger.

Full reasoning: Type System Discipline and Boundary Discipline in `../goblin-mode/references/principles.md`.
