---
name: structure-first
description: "Use for code generation, feature work, bug fixes, refactoring, and code review when a change creates or reshapes a multi-step flow, state lifecycle, side-effect or decision ownership, cross-unit composition, or boundary contract. Also use it when an existing structural problem makes those elements hard to trace or verify. Structural change is optional. Mechanical edits, throwaway experiments, and coherent local changes stay with their current owner and focused verification."
---

# Skill: Structure First

## Purpose

> **Primary Flow**: a top-down readable main path for logic whose natural form is imperative orchestration

Keep the relevant behavior readable in the form natural to that code. Make responsibilities, composition, effects, state, and verification clear enough to understand, change, and verify the requested behavior. Use a Primary Flow, an Atom, a composition point, or a side-effect boundary when it makes the relevant behavior clearer.

Prefer changes that remove complexity or isolate it behind a genuinely independent responsibility. Keep the existing structure when it already supports a coherent change, and secure changed behavior with **contract-driven tests** rather than implementation-following tests.

## Application

- Use it for code generation, feature work, bug fixes, refactoring, and code review when a change creates or reshapes a flow, state lifecycle, effect or decision ownership, cross-unit composition, or boundary contract. Existing structural problems that obscure those elements also call for this skill.
- Apply it lightly when the current structure is already clear.
- For planning, classification, or scope analysis, keep it as an internal lens rather than a response template.
- For user-visible bugs or UI malfunctions, characterize the observable behavior first; apply structure work only after the current unit's responsibility for that behavior is clear.
- Keep mechanical edits, throwaway experiments, and coherent local changes with their current owner and focused verification.

## Core Bias

- Traceable behavior and ownership > structural simplicity > reusability > abstraction
- Prefer **clarity of the current code** over speculative future needs.
- Keeping, inlining, merging, deleting, reordering, and extracting are all valid outcomes.

## Operating Model

Pick the smallest **current unit** responsible for the behavior or rule being changed, not merely where its symptoms or outputs appear.
Local changes usually mean function/file. Feature work usually means module/use case. Larger refactors may mean capability/subsystem.

1. **Trace the behavior**
- State the intent and smallest observable completion condition in one sentence.
- Follow the behavior in the reading form natural to the code: for example, an imperative flow, state transition, event lifecycle, rule set, dataflow, or protocol boundary.
- Include call sites, types, tests, documentation, and configuration only when leaving them unchanged would break the requested behavior, a contract, or meaningful verification. Exclude adjacent cleanup.

2. **Name the structural demand or friction**
- Name the structural demand created or reshaped by the change. It may involve a flow, state transition or lifecycle, effect or completion ownership, composition, or boundary contract.
- Also name any existing problem that makes the behavior hard to trace, change, or verify.
- When the current unit already owns the change and its focused verification, keep the work within that unit.

3. **Explore only meaningful structural choices**
- Compare a local clarification with a structural change only when both are credible.
- Treat keeping, inlining, merging, deleting, reordering, and extracting as equal candidates.
- A Primary Flow may clarify imperative orchestration. An Atom is an independently understandable role whose behavior can change without coordinating unrelated responsibilities; size, purity, and extraction are possible evidence, not requirements.
- Make composition discoverable at its natural owner and keep unrelated decisions or lifecycles with their own owners.
- Make effect ownership and failure meaning visible. Isolate an effect at a separate boundary only when doing so materially improves reasoning, verification, retry, or replacement.

4. **Choose by total effect**
- Select a structural change when it removes complexity or usefully isolates it behind an independent responsibility.
- Check the complete path through helper chains, wrappers, context objects, configuration, state, error channels, and lifecycle to confirm where complexity now lives.
- Request a user decision when the unresolved choice needs user authority or would make a hard-to-reverse public API, data, security, dependency/cost, or migration commitment. Use and report a reversible local assumption for other unresolved choices.

## Growth and Ownership

- Start with the minimum public I/O/signature for the confirmed responsibility; grow it only when responsibility changes (new external input, mixed semantics, or boundary move).
- Do not add options, configuration, dependencies, or abstractions for unconfirmed future use; remove code made unused by the current change.
- Give each policy, decision, or calculation rule a non-competing resolution path: one owner, an explicit order of composition, or a coordination/conflict-resolution protocol.
- Make externally visible write ownership discoverable. When multiple writers are intentional, make their coordination or conflict contract visible rather than centralizing them by default.
- At larger scales, make the relevant entrypoints, composition or coordination, and decision resolution discoverable.
- Make the freshness and completion resolution path at async boundaries explicit; it may be one owner or a protocol.
- If rule ownership changes or you introduce an equivalent new path, remove/disable the old one in the same change when possible. Otherwise include a staged migration plan (owner, exit condition).
- `Decision rule`: repeated predicate, weight, priority, policy, calculation, or key-generation logic that decides behavior.
- `Equivalent path`: an alternative execution path that yields the same externally observable result.

## Testing

- Write **sufficient tests at the most stable responsible unit available** whenever possible.
- Validate **contracts (I/O, invariants, edge cases)** between the current unit and its owned roles or boundaries, not internals.
- Match verification to risk and change type: reproduce or characterize bugs before changing them, verify stable behavior before and after refactors, and cover feature success, failure, and relevant boundaries. Narrow the failure before changing several plausible causes; if checks cannot run, state why and name the next useful check.
- If orchestration or boundary integration is where the risk lives, test the current unit directly.
- For async or stateful boundaries, test ownership contracts such as stale-result handling, balanced completion, and equivalent-input no-op at the most stable unit that owns them.
- If tests cannot be added in the current change, say so explicitly and name the next stable responsible unit(s) plus the required contract cases.
- Keep test code readable: use `each`/table cases to reduce duplication, allow only small helpers that do not blur structure, and keep each test focused on one core assertion.

## Anti-Patterns

- If splitting increases argument/state passing, roll it back.
- Do not split functions/files for appearance only (avoid utility sprawl).
- Do not shorten the top level by displacing complexity into helper chains, wrappers, context objects, configuration, hidden state, error channels, or additional lifecycle.
- If names start turning into long explanations, re-check boundaries.
- Avoid adding abstractions/layers for assumed future reuse.
- Avoid over-abstracted tests and helper sprawl.
- Do not add parameters "for later."
- Do not keep the same policy, decision, calculation, or key-generation rule in multiple owner locations.
- Do not split the same externally observable result across multiple writer locations unless coordinating those writers is itself the explicit responsibility.
- Do not synchronously mirror upstream boundary state into local mutable state unless ownership and reset semantics are explicit.
- Do not create self-feedback loops where a unit reads from an input/update path and writes back into that same path.
- Do not keep new and legacy equivalent paths in parallel without a staged migration plan (owner, exit condition).

## Risk-Matched Review

Use only the questions relevant to the current change:

- Is the relevant behavior and decision ownership easier to trace?
- Was complexity removed or isolated behind an independent responsibility, rather than moved into helpers, wrappers, context, state, error channels, or lifecycle?
- Does each new boundary correspond to a real responsibility, effect, or contract?
- Does verification protect the changed observable behavior and contracts?

## Optional Completion Evidence

Use this template only when structure itself is the point; otherwise answer naturally.

When the format is useful, provide these lines:

- `Current Unit:` function/file | module/use case | capability/subsystem
- `Structural Demand:` the changed flow, state, effect, ownership, composition, or contract; an existing structural problem; or `none; structure unchanged`
- `Readable Behavior:` the natural causal/read form after the change
- `Structural Choice:` kept | inlined | merged | deleted | reordered | extracted, with the reason
- `Tests:` `added ...` or `deferred because ...; next stable unit(s): ...; required contract cases: ...` (include freshness/completion contract when relevant)

For refactoring work where rule ownership changed, also provide:

- `Decision Ownership:` `policy/decision/calculation/key-generation rule -> owner unit`; duplicated owner removed? yes/no

For refactoring work where signatures/boundaries grew or an old path was replaced, also provide:

- `Refactor Check:` parameter growth reason / legacy path status (removed, disabled, migration plan)
