# Verification

Use this detail when risk lives at a boundary or the runtime contract needs evidence beyond a local helper.

Test observable contracts at the most stable responsible unit, not helper internals. Trace a derived decision or output back through its assignments and guards to the source facts that justify it or require its visibility; supplying the derived value tests only its consumer. For history-dependent meaning, identify what each implicated unit retains and what prior evidence makes its comparisons valid. Hold the contract-relevant source events fixed and vary a reachable observation history to challenge whether changed knowledge alone can yield an unsupported conclusion. Trace or exercise only the implicated producer-to-consumer path, reusing evidence that covers the same path and history. Include a valid contrasting case when needed to rule out blanket rejection or suppressed output.

When cross-representation drift of a settled meaning is material, include a representative case at the first point where another unit could reinterpret it. For material claims across identity, authoritative data, cross-representation meaning, external writes, or runtime/async boundaries, use the nearest safe witness from that boundary’s owner. Do not automatically require production or full end-to-end checks.

Match checks to risk and change type:

- Reproduce or characterize a bug before fixing it. Narrow the failure before changing several plausible causes.
- Preserve stable behavior across a refactor.
- Cover feature success, failure, and relevant boundaries.
- At async or stateful boundaries, verify the current contracts affected by the change at their owning unit. Stale-result handling, balanced completion, and equivalent-input no-op are candidate checks only where that behavior is required.

For deployment, resolve the existing credential/configuration owner and exact target, effects, and recovery path before applying. Verify the user’s access path in the deployed environment; local or fixture success does not close that boundary.

When recording or materially extending a finding, compare its consequential claims with the actual witness inputs and observations. If reproduction is required or chosen, select the supported contract violation that determines the finding's significance, rather than an easier symptom sharing its cause. If the witness lacks that consequence's qualifying facts, adapt and safely execute it before optional broader checks, reusing supported setup.

Source reasoning may suffice for further consequences whose material premises and path are established. Execution is still needed when explicitly required or when a decision-relevant boundary premise remains unsettled. Do not require a run for every implication or field, or rebuild an undisputed producer chain. Distinguish source-backed conclusions from executed results and retain unavailable required checks as unmet. Derive completion claims from tested scope, source/target identity, environment, fixture dependencies, and unmet acceptance criteria. Reuse valid evidence.

Keep tests readable and focused. If no safe witness is available or current witnesses conflict, leave the boundary unresolved. Name the next check, responsible unit, and required cases; local tests do not close it.
