# Verification

Use this detail when risk lives at a boundary or the runtime contract needs evidence beyond a local helper.

Test sufficient observable contracts at the most stable responsible unit: I/O, invariants, edge cases, and owned boundary behavior. Do not lock down helper internals. Test orchestration or integration at the current unit when that is where risk lives.

When cross-representation drift of a settled meaning is material, include a representative case at the first point where another unit could reinterpret it. For material claims across identity, authoritative data, cross-representation meaning, external writes, or runtime/async boundaries, use the nearest safe witness from that boundary’s owner. Do not automatically require production or full end-to-end checks.

Match checks to risk and change type:

- Reproduce or characterize a bug before fixing it. Narrow the failure before changing several plausible causes.
- Preserve stable behavior across a refactor.
- Cover feature success, failure, and relevant boundaries.
- At async or stateful boundaries, verify stale-result handling, balanced completion, and equivalent-input no-op at the unit that owns those contracts.

For deployment, resolve the existing credential/configuration owner and exact target, effects, and recovery path before applying. Verify the user’s access path in the deployed environment; local or fixture success does not close that boundary.

Derive completion claims from check results: tested scope, source/target identity, environment, fixture dependencies, and unmet acceptance criteria. Reuse valid evidence rather than adding a fixed review chain.

Keep tests readable and focused. If no safe witness is available or current witnesses conflict, leave the boundary unresolved. Name the next check, responsible unit, and required cases; local tests do not close it.
