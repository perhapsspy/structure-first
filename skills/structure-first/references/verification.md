# Verification

Use this detail when risk lives at a boundary or the runtime contract needs evidence beyond a local helper.

Test sufficient observable contracts at the most stable responsible unit: I/O, invariants, edge cases, and owned boundary behavior. Do not lock down helper internals. Test orchestration or integration at the current unit when that is where risk lives.

When cross-representation drift of a settled meaning is material, include a representative case at the first point where another unit could reinterpret it. For material claims across identity, authoritative data, cross-representation meaning, external writes, or runtime/async boundaries, use the nearest safe witness from that boundary’s owner. Do not automatically require production or full end-to-end checks.

Match checks to risk and change type:

- Reproduce or characterize a bug before fixing it. Narrow the failure before changing several plausible causes.
- Preserve stable behavior across a refactor.
- Cover feature success, failure, and relevant boundaries.
- At async or stateful boundaries, verify stale-result handling, balanced completion, and equivalent-input no-op at the unit that owns those contracts.

Keep tests readable and focused. If no safe witness is available or current witnesses conflict, leave the boundary unresolved. Name the next check, responsible unit, and required cases; local tests do not close it.
