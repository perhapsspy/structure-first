# Reviewing Across Owners

Use this procedure for a requested bug review spanning several responsible units and their composed contracts. Focused local reviews use the ordinary contract trace and checks.

## Shared budget and transition

Use the invocation's original start and any explicitly supplied wall-time or exec caps. Setup, reads, checks, waits, checkpointing, challenge, and integration share them. Do not ask for missing caps or invent an overall limit.

For each supplied cap, begin checkpointing at 45% and finish checkpointing and the deferred read by 50%; the first 45% threshold reached triggers transition. With no caps, set a provisional draft work allocation at the start for concrete investigation and checks, reserving effort for challenge and integration, and switch at its end. This allocation is not an overall hard cap or a reason to finish the review. Bound operations and waits to leave room for transition.

From the first substantive observation, maintain the requested review deliverable as an in-progress checkpoint. If none is requested, use the existing permitted review notes. Separate findings from open questions. For each material open question, retain the exact undecided promised outcome, its current premises or concrete data, and the next deciding action. Update the affected entry in place; do not rebuild the pending set from a newer summary or maintain a second task ledger.

At transition, save the actual hypotheses, dismissals, coverage limits, probe and evidence locations, and unresolved premises in that checkpoint. Preserve unfinished or failed attempts; success is not required to switch, and unfinished work does not extend the draft allocation. Do not polish or rerun checks merely to package it.

Then read [Review Challenge](review-challenge.md) through the native file tool. Do not preload either language version, including through bulk reference reads. Continue directly within this invocation and any original caps; there is no budget reset.

## Draft investigation

Generate questions from the original contract's condition–outcome obligations. Locate the decision, effect, or public result for a selected material obligation across its supported entries, and read the clauses that jointly qualify that result. Preserve their qualifiers and logical direction. Do not restrict starting points to writers, control operations, or findings already in the notes.

Before choosing fixture data, work backward through the result's decisive conditions. For each distinct contractual premise, inspect the actual assignments and transformations producing the evidence the consumer relies on. A producer may compute or interpret a value without performing a write. State what its evidence establishes and what the consumer requires that evidence to mean. Continue through a derived claim until its meaning rests on supported source facts and invariants, or a specific unsupported implication becomes a deciding question. A field name, successful write, present guard, or correct reaction to a seeded value does not establish that implication. Investigate the missing implication before building a larger scenario around it.

At stateful boundaries, follow retained facts through their write, preserve, and clear paths into downstream decisions and public readers. Prior unsuccessful or unfinished work can leave independently valid facts even when the current operation or primary mode differs. Use a supported history in which the selected obligation remains active. Apply Verification to disputed derivations and histories; reuse supported seeds where production is undisputed.

Attempt the smallest reachable counterexample at the selected relation: an outcome without its contractual justification, or a required outcome suppressed despite valid qualifying facts. Check upstream invariants and alternate paths. Perform a bounded source comparison or safe focused probe, record the actual evidence and unfinished next action in the existing working report, and select again. Inspect the selected result's contractual premises, not every implementation field; reuse established paths and do not require execution for every clause. Develop an evidence-bearing draft within the allocation, carrying unfinished work into the challenge without extending it.
