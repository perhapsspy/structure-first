# Reviewing Across Owners

Use this procedure for a requested bug review spanning several responsible units and their composed contracts. Focused local reviews use the ordinary contract trace and checks.

## Draft investigation

Work backward from the requested effects and public results, including read-only results, to the owners supplying and interpreting their facts. Identify distinct producer–consumer–promised-outcome boundaries in a small temporary note. Merge equivalent obligations without combining different outcomes merely because they share a feature name.

For a material boundary, state the contract's permission or required outcome using source facts/history, separately from the implemented guards and data/evidence transformations. Try a reachable counterexample: code producing a forbidden outcome, or omitting or misrepresenting a required outcome. Check upstream invariants and alternate paths. Record the attempted assignment and its result or unresolved premise. Normal success alone does not establish the boundary's contract. Use the existing Verification rules for focused witnesses.

Return the actual draft, notes, tests, and results at the draft phase's boundary. This return is an intermediate result for the review owner, who carries the challenge and integration through before the user-facing completion.

## Evidence challenge

Run this as a separate review invocation. For delegated reviews, continue the same reviewer with the original task, complete contract, source, and actual draft artifacts. Prior notes, reports, and tests are claims and evidence, not a definition of scope or a trusted contract model.

Start from material promises attached to the requested effects and public results, including promises omitted from the prior artifacts. Select an unexamined promise or an unsupported claim of coverage. State the required contractual fact with its source anchor, then state separately what the existing code and test evidence actually establishes. Trace the missing inference through the responsible producers and consumers. Try a reachable counterexample and use a focused probe where needed. An implementation label or a successful related case does not establish the missing fact.

Reuse valid witnesses rather than routinely reproducing established findings. For each investigated challenge, record only the promise, existing evidence, missing inference, and result. Amend the combined report, retaining findings not refuted by evidence and distinguishing discovery from executed reproduction. Apply the existing boundary evidence rules; a challenge does not automatically require a full runtime or end-to-end test.

## Shared budget and completion

Reserve part of the current review budget for the challenge. Count investigation, handoff, waiting, and challenge together; the challenge does not receive a new full budget. Pass the actual remaining budget at the phase boundary. Preserve the configured model and effort.

The review owner integrates the combined findings against the original request and actual evidence. Source exposure, generic assurances, and finding counts do not establish coverage. Report the checked paths, supplied facts, generated facts, and remaining limits. Keep these working notes temporary unless the task requires a durable record.
