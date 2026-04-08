---
name: structure-first
description: Readable primary-flow–first code structuring with minimal boundaries, atomic composition, and contract-driven unit tests
license: MIT
metadata:
  author: perhapsspy@gmail.com
  version: '1.0'
  source_repository: https://github.com/perhapsspy/structure-first
---

# Skill: Structure First

## Purpose

> **Primary Flow**: the top-down readable main path that orchestrates the logic

When generating, refactoring, or reviewing code, prioritize a **readable success path (Primary Flow)** first.
Keep boundaries minimal (only when needed), compose with **Atoms** (small units with one stable role and clear I/O), and secure stability through
**contract-driven tests** rather than implementation-following tests.

## Use / Do Not Use

- Use this skill when the **code shape itself is changing** or when you are doing a structure-focused code review.
- For planning, classification, or scope analysis, keep it as an internal lens rather than a response template.
- Use it when code does not read naturally from top to bottom.
- Use it when function/module splitting becomes excessive and utilities start to spread.
- Use it when tests are drifting toward implementation-following patterns.
- Do not use it for throwaway experiments or one-off exploratory code.
- Do not use it for tiny changes where structural intervention would be excessive.

## Core Bias

- Readable flow > structural simplicity > reusability > abstraction
- Prefer **clarity of the current code** over speculative future needs.
- Splitting is not a goal; split only when readability clearly improves.

## Operating Model

Pick one **current unit** and make that unit readable before moving outward.
Local changes usually mean function/file. Feature work usually means module/use case. Larger refactors may mean capability/subsystem.

1. **Fix Intent**
- State the intent of the change/code in one sentence.
- State the current unit before restructuring: function/file, module/use case, or capability/subsystem.

2. **Minimize Boundaries**
- Classify steps as I/O, domain decision, or transform.
- Do not add more boundaries than necessary.

3. **Primary Flow First**
- Make the success path readable in one top-down pass.
- Keep branches/exceptions from breaking the main flow (early return or push them downward).
- A good result often still reads like `normalize -> load -> decide -> return`.
- When flattening local branch logic, preserve whether rules are cumulative or precedence-ordered.

4. **Extract Atoms**
- Split when a Primary Flow sentence becomes clearer as a function or child unit.
- Atoms do one stable job; their I/O should be describable in one line.
- Prefer pure functions when possible.
- At function/file scale, stop when splitting no longer clarifies the local flow.

5. **Keep Composition in One Place**
- Keep orchestration in one place at the current unit.
- Minimize direct dependencies/calls between Atoms.

6. **Push Side Effects to Boundaries**
- Gather side effects (I/O, state mutation) at boundaries.
- Keep inner logic focused on computation and decisions.

7. **Align Read Order**
- At file level, default to: export/public -> orchestrator -> atoms -> utils for top-down discoverability.
- If branch narration starts depending on extra intermediate data structures or helper chains, keep more inline or stop descending.

## Growth and Ownership

- Start with the minimum public I/O/signature for the confirmed responsibility; grow it only when responsibility changes (new external input, mixed semantics, or boundary move).
- One policy, decision, or calculation rule, one owner.
- One externally visible write path, one owner. If coordinating multiple writers is itself the responsibility, make that coordinator explicit.
- At larger scales, make the entrypoint, main orchestrator, and decision owners visible.
- Async boundaries should have one owner for freshness and completion policy.
- If rule ownership changes or you introduce an equivalent new path, remove/disable the old one in the same change when possible. Otherwise include a staged migration plan (owner, exit condition).
- `Decision rule`: repeated predicate, weight, priority, policy, calculation, or key-generation logic that decides behavior.
- `Equivalent path`: an alternative execution path that yields the same externally observable result.

## Testing

- Write **sufficient tests at the most stable Atom level available** whenever possible.
- Validate **contracts (I/O, invariants, edge cases)** between the current unit and its Atoms/boundaries, not internals.
- If orchestration or boundary integration is where the risk lives, test the current unit directly.
- For async or stateful boundaries, test ownership contracts such as stale-result handling, balanced completion, and equivalent-input no-op at the most stable unit that owns them.
- If tests cannot be added in the current change, say so explicitly and name the next stable Atom(s) plus the required contract cases.
- Keep test code readable: use `each`/table cases to reduce duplication, allow only small helpers that do not blur structure, and keep each test focused on one core assertion.

## Anti-Patterns

- If splitting increases argument/state passing, roll it back.
- Do not split functions/files for appearance only (avoid utility sprawl).
- If names start turning into long explanations, re-check boundaries.
- Avoid adding abstractions/layers for assumed future reuse.
- Avoid over-abstracted tests and helper sprawl.
- Do not add parameters "for later."
- Do not keep the same policy, decision, calculation, or key-generation rule in multiple owner locations.
- Do not split the same externally observable result across multiple writer locations unless coordinating those writers is itself the explicit responsibility.
- Do not synchronously mirror upstream boundary state into local mutable state unless ownership and reset semantics are explicit.
- Do not create self-feedback loops where a unit reads from an input/update path and writes back into that same path.
- Do not keep new and legacy equivalent paths in parallel without a staged migration plan (owner, exit condition).

## Final Gates

- Can the success path be seen in one top-down read?
- Is the current unit stated clearly and still the right unit for this change?
- At function/file scale, is the flow still shallow enough without extra intermediate data structures or helper chains narrating the branches?
- Does splitting reflect real responsibility/boundary changes?
- Can each Atom's I/O be explained in one line?
- Are side effects concentrated at boundaries?
- Are tests contract-focused and concise?
- At capability/subsystem scale, can you name the entrypoint, main orchestrator, and decision owners?
- If more structure work remains across units, is the next re-entry point clear before ending this pass?
- Are parameter growth and old-path handling (cleanup or staged migration) justified and complete?

## Optional Completion Evidence

Use this template only when structure itself is the point; otherwise answer naturally.

When the format is useful, provide these four lines:

- `Current Unit:` function/file | module/use case | capability/subsystem
- `Primary Flow:` top-down in 3-6 lines
- `Boundaries:` list of I/O boundaries
- `Tests:` `added ...` or `deferred because ...; next stable Atom(s): ...; required contract cases: ...` (include freshness/completion contract when relevant)

For refactoring work where rule ownership changed, also provide:

- `Decision Ownership:` `policy/decision/calculation/key-generation rule -> owner unit`; duplicated owner removed? yes/no

For refactoring work where signatures/boundaries grew or an old path was replaced, also provide:

- `Refactor Check:` parameter growth reason / legacy path status (removed, disabled, migration plan)
