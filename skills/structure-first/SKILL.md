---
name: structure-first
description: "Use for code generation, feature work, bug fixes, refactoring, and code review when a change creates or reshapes a multi-step flow, state lifecycle, side-effect or decision ownership, cross-unit composition, or boundary contract. Also use it when an existing structural problem makes those elements hard to trace or verify. Structural change is optional. Mechanical edits, throwaway experiments, and coherent local changes stay with their current owner and focused verification."
---

# Structure First

Find the owner. Trace the flow. Change the smallest responsible unit. Verify the contract.

## Runtime Contract

1. Choose the smallest **current unit** that owns the behavior or rule, not merely its symptom or output. State the intent and minimum observable completion condition. For a bug, establish the observable failure before restructuring.
2. Trace only the needed path from caller through decision or state and write or effect to completion, using the form natural to the code. Include types, tests, docs, and config only when leaving them unchanged would break the behavior, contract, or meaningful verification.
3. Name the structural demand—flow, lifecycle, decision/effect/completion ownership, composition, migration, or boundary contract—and the friction that blocks tracing or testing.
4. Prefer focused local clarification. Change structure only when it removes total complexity or isolates an independently changeable responsibility; a shorter top level is not better when helpers, wrappers, context, state, errors, or lifecycle merely hide the complexity.
5. Give each decision, writer, effect, and completion rule one discoverable, non-competing resolution path. Remove an old equivalent path in the same change; otherwise name the migration owner and exit condition.
6. Verify observable behavior at the most stable responsible unit, not helper internals. Reopen only the smallest implicated unit when evidence shows that another unit owns part of the contract.

Keeping, inlining, merging, deleting, reordering, extracting, and making no structural change are all valid outcomes. Do not add future-use options, configuration, dependencies, wrappers, or abstractions.

## Required Detail

Read [Structural Boundaries](references/structural-boundaries.md) before changing public I/O; decision, writer, effect, or completion ownership; async/state lifecycle; representation meaning; or migration paths.

Read [Verification](references/verification.md) when a material claim crosses identity, authoritative data, representations, external writes, or runtime/async boundaries, or when a bug, refactor, or feature needs boundary evidence.

Report the current unit, structural demand, chosen outcome, ownership or migration status, and verification only when they help the task. Do not force a template onto planning or simple local work.
