# Code smells

Catalogue: https://sourcemaking.com/refactoring/smells

## Bloaters

| Smell | Sign | Move |
| --- | --- | --- |
| Long Method | needs section comments to follow | extract by step |
| Large Class | module changes for unrelated reasons | split by reason |
| Primitive Obsession | same literal union or id rule retyped | named type |
| Long Parameter List | 3+ params, or two of one type | object argument |
| Data Clumps | same values travel together | one type |

## Object-orientation abusers

| Smell | Sign | Move |
| --- | --- | --- |
| Switch Statements | same switch in several places | one table or dispatch |
| Temporary Field | optional fields valid only in one mode | union with `kind` |
| Refused Bequest | subclass ignores what it inherits | composition |
| Alternative Classes, Different Interfaces | two modules, same job | one interface |

## Change preventers

| Smell | Sign | Move |
| --- | --- | --- |
| Divergent Change | one file edited for many reasons | split by reason |
| Shotgun Surgery | one rule change edits many files | give it an owner |
| Parallel Inheritance | new subclass forces a twin | merge hierarchies |

## Dispensables

| Smell | Sign | Move |
| --- | --- | --- |
| Comments | explains what code does | rename or extract; keep the why |
| Duplicate Code | copy that must change together | owner |
| Lazy Class | fails the deletion test | inline |
| Data Class | callers apply its rules | move rules in; plain types are fine |
| Dead Code | no production caller (search all packages and scripts) | delete; retarget its tests |
| Speculative Generality | hook for a future nobody scheduled | delete; ask if a roadmap may need it |

## Couplers

| Smell | Sign | Move |
| --- | --- | --- |
| Feature Envy | works mostly on another module's data | move it there |
| Inappropriate Intimacy | writes another module's tables or internals | go through its interface |
| Message Chains | `a.b().c().d()` | ask the first object |
| Middle Man | only forwards calls | remove |

## Other

| Smell | Sign | Move |
| --- | --- | --- |
| Incomplete Library Class | same library workaround repeated | one adapter |
