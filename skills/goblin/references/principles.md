# Principles (condensed from pstack)

Read only the entry you need.

## Core

**Laziness Protocol.** Smallest change that solves it. One source of truth per decision, passed as a simple value. Fewer lines beat elegant boilerplate.

**Foundational Thinking.** Data shape before logic: define core types, trace access patterns, pick structures for dominant paths. DRY structure, not every line; three similar statements beat a premature abstraction. Scaffold (CI, tests, shared types) first when every later step benefits. Before sharing state between actors ask "what if another actor changes this?"; if not "nothing", isolate.

**Redesign from First Principles.** New requirement → ask "if built from scratch with this, what would we build?" Read all affected files, propagate change through types, docs, examples. Deliver incrementally.

**Attack the Premise.** Two+ fixes sharing one premise failed same gate → write premise as one sentence, find an observation that differs if it's false, run it. Contradicted → cause is elsewhere.

**Subtract Before You Add.** Remove dead code, redundant validators, stubs first, then build. Design for observed usage, not speculative edges. No guards beyond spec.

**Minimize Reader Load.** Two axes: layers to trace, state to hold. Collapse one-caller wrappers and single-impl adapters. Shrink mutable scope. LOC and "clean architecture" are proxies.

**Outcome-Oriented Execution.** Planned rewrites: converge on target, don't build throwaway compat code. Planned, scoped, reversible breakage mid-migration is OK. Full static + runtime check at end.

**Experience First.** User delight over implementation convenience. Ship fewer polished things. User = whoever consumes it, incl. library callers and next maintainer.

**Exhaust the Design Space.** Novel interaction or architecture with no precedent → 2-3 cheap throwaway sketches, compare, then commit.

**Build the Lever.** Non-trivial work → build the codemod/script/check that does or proves it. Do first unit by hand, then script it and diff against hand result. Make it safe to rerun. Skip for a couple of obvious edits.

## Architecture

**Model the Domain.** Encode domain in a structure: state machine over booleans, typed model over loose params, table/registry/union over branching across files, reducer over ad hoc mutation, module per body of knowledge (not per pipeline step).

**Boundary Discipline.** Validate and handle errors at boundaries (CLI, config, network, external APIs). Inside: typed data, no re-validation. Business logic pure; shell thin.

**Type System Discipline.** Illegal states unrepresentable. Brand semantic primitives (UserId ≠ OrderId). External data untyped until parsed at boundary. Exhaust variants. Derive types from authoritative schema.

**Make Operations Idempotent.** Each step reads current state, compares to goal, applies only the difference. Leftovers (locks, temp files, claimed jobs) must be recognizable and recoverable. Ask "runs twice? crashed halfway?"

**Migrate Callers Then Delete Legacy APIs.** New internal API → migrate all callers and delete old one in same wave. Update tests to new contract. Applies when no external users need compat.

**Separate Before Serializing Shared State.** Concurrent writers → first remove sharing (own file/key/branch each, merge at read). Real shared invariant → enforce structurally (lock, sequential phase, single owner). Conventions aren't concurrency control.

## Verification

**Prove It Works.** Check the real thing: run it, read actual value, inspect diff. Not mtimes, self-reports, "compiles". Verification fails → suspect the observation method first. Script the check when possible.

**Fix Root Causes.** Reproduce. Ask "why" until answer is a wrong decision in code. Instrument, don't guess. If triggering state is legitimate, the code that broke on it is the root cause. A guard is a fix only for legitimate states.

**Sequence Verifiable Units.** Small units, each ending in a check; don't advance until green. Order commits so history proves the work (failing test, then fix).

**Test Behavior, Not Implementation.** Assert what users observe (return, error, readable state, external effect). Imagine breaking the behavior: test must fail. Imagine refactoring internals: test must pass.

**Explain the Number.** Name the limiter (core, lock, disk, network, load generator) from profile/counters, not code reading. List what else it could measure (errors, cached work, code not run, untuned side, noise) and rule each out. Keep run count + spread with the number.

## Delegation

**Guard the Context Window.** Bulk output, long files, repeated reads → one subagent, summary back. Cap scope per phase.

**Never Block on the Human.** Reversible → proceed, then present. Irreversible → confirm. Product direction comes from human; execution doesn't wait.

## Meta

**Encode Lessons in Structure.** Same instruction twice → make it a lint, type, runtime check, or script. Can't encode (needs judgment) → make instruction prominent + add failure example.
