---
name: structure-first
description: "Use for code generation, feature work, bug fixes, refactoring, and code review when a change creates or reshapes a multi-step flow, state lifecycle, side-effect or decision ownership, cross-unit composition, or boundary contract. Also use it when an existing structural problem makes those elements hard to trace or verify. Structural change is optional. Mechanical edits, throwaway experiments, and coherent local changes stay with their current owner and focused verification."
---

# Structure First

## Purpose and Boundaries

Make the requested behavior readable, changeable, and verifiable in the form natural to the code. Prefer traceable behavior and ownership over structural simplicity, reuse, or abstraction. Structural change is optional: keeping, inlining, merging, deleting, reordering, and extracting are all valid outcomes.

Keep mechanical edits, throwaway experiments, and coherent local changes with their current owner. For user-visible bugs, establish the observable failure and its responsible current unit before restructuring.

Unsettled product purpose belongs to purpose-fit design; cross-representation meaning ownership to semantic boundary design; pure async interaction and freshness to interactive-state flow. Use those workflows when available. In a standalone installation, state the missing prerequisite and resolve it only within explicit user authority. Consume settled contracts without reopening them; if one remains unsettled, do not invent its implementation mechanics here.

## Structural Contract

Choose the smallest **current unit** that owns the behavior or rule, not merely its symptom or output. State the intent and smallest observable completion condition, then trace the natural reading form: imperative flow, state transition, event lifecycle, rule set, dataflow, or protocol boundary. Include callers, types, tests, docs, and config only when leaving them unchanged would break the requested behavior, its contract, or meaningful verification.

Name the structural demand created or reshaped by the change—flow, lifecycle, effect/completion ownership, composition, or boundary contract—and any existing friction that blocks tracing or testing. Use focused verification to keep work within the current unit. Reopen only the smallest implicated unit when evidence shows that another unit owns a decision, write, effect, or completion rule.

Compare local clarification with structural change only when both are credible. A **Primary Flow** is the top-down readable main path for imperative orchestration; keep branches and exceptions from obscuring its main causal path. An **Atom** is an independently understandable role whose behavior can change without coordinating unrelated responsibilities. Neither is a required extraction.

Choose by total effect. Change structure only when it removes complexity or usefully isolates it behind an independent responsibility. Inspect the complete path through helpers, wrappers, context objects, configuration, state, error channels, and lifecycle; a shorter top level is not an improvement if complexity merely moved.

Keep composition discoverable at its natural owner. Keep unrelated decisions and lifecycles with their own owners. Make effect ownership and failure meaning visible; isolate an effect only when the boundary materially improves reasoning, verification, retry, or replacement.

Ask for a user decision when an unresolved choice needs user authority or creates a hard-to-reverse public API, data, security, dependency/cost, or migration commitment. For other unresolved choices, use and report a reversible local assumption.

## Ownership and Migration

- Start public I/O and signatures at the minimum confirmed responsibility. Grow them only for a real new external input, mixed meaning, or boundary move; do not add future-use options, configuration, dependencies, or abstractions.
- Give each policy, decision, calculation, priority, or key-generation rule a non-competing resolution path: one owner, explicit composition order, or a coordination/conflict protocol.
- Make externally visible write ownership discoverable. Allow multiple writers only when coordinating them is an explicit responsibility with a discoverable owner or protocol; otherwise keep one writer. Do not centralize intentional writers automatically.
- At async boundaries, make freshness and completion resolution explicit as an owner or protocol. Do not mirror upstream boundary state into local mutable state without explicit ownership/reset semantics, or create a self-feedback loop through the same input/update path.
- Remove code made unused by the change. When rule ownership moves or an equivalent execution path is introduced, remove or disable the old path in the same change when possible; otherwise provide a staged migration owner and exit condition.

## Verification

Test sufficient observable contracts at the most stable responsible unit: I/O, invariants, edge cases, and owned boundary behavior—not helper internals. For material claims across identity, authoritative data, external writes, or runtime/async boundaries, use the nearest safe witness from that boundary’s owner without automatically requiring production or full end-to-end checks. Test orchestration or integration at the current unit when that is where risk lives.

Match checks to risk and change type. Reproduce or characterize a bug before fixing it; preserve stable behavior across refactors; cover feature success, failure, and relevant boundaries. Narrow the failure before changing several plausible causes.

For async or stateful boundaries, verify stale-result handling, balanced completion, and equivalent-input no-op at the unit that owns those contracts. Keep tests readable and focused. If no safe witness is available, leave the boundary unresolved and name the next check, responsible unit, and cases; local tests do not close it.

Report structural evidence only when it helps the task: current unit, structural demand, chosen outcome, decision ownership or migration status, and verification. Do not force a template onto planning or simple local work.
