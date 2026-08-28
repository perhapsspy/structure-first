# Structural Boundaries

Use this detail after the runtime contract identifies a change to ownership, lifecycle, public I/O, representation, or migration.

## Scope and Decisions

Make requested behavior readable, changeable, and verifiable in the form natural to the code. Prefer traceable behavior and ownership over structural simplicity, reuse, or abstraction.

Keep mechanical edits, throwaway experiments, and coherent local changes with their current owner. For user-visible bugs, establish the observable failure and responsible current unit before restructuring.

Treat settled product purpose, domain meaning, and async interaction or freshness decisions as inputs. Do not reopen them. If one remains unsettled, do not invent its implementation mechanics. Ask for a user decision when the choice needs user authority or creates a hard-to-reverse public API, data, security, dependency/cost, or migration commitment. Otherwise use and report a reversible local assumption.

## Shape and Total Effect

Use the code's natural reading form: imperative flow, state transition, event lifecycle, rule set, dataflow, or protocol boundary.

A **Primary Flow** is the top-down readable main path for imperative orchestration; branches and exceptions should not obscure its causal path. An **Atom** is an independently understandable role whose behavior can change without coordinating unrelated responsibilities. Neither requires extraction.

Compare local clarification with structural change only when both are credible. Inspect the complete path through helpers, wrappers, context objects, configuration, state, error channels, and lifecycle. Change structure only when it removes complexity or usefully isolates it behind an independent responsibility.

Keep composition discoverable at its natural owner and unrelated decisions and lifecycles with their own owners. Make effect ownership and failure meaning visible. Isolate an effect only when the boundary materially improves reasoning, verification, retry, or replacement.

## Ownership Rules

- Start public I/O and signatures at the minimum confirmed responsibility. Grow them only for a real new external input, mixed meaning, or boundary move.
- Give every policy, decision, calculation, priority, and key-generation rule a non-competing resolution path: one owner, explicit composition order, or a coordination/conflict protocol.
- When one settled domain meaning crosses representations and drift is a material risk, keep its interpretation with the owning unit. Other units may transport, project, or apply an explicitly scoped compatibility translation, but must not independently infer or reinterpret it.
- Make externally visible write ownership discoverable. Multiple writers are valid only when their coordination has an explicit, discoverable owner or protocol. Do not centralize intentional writers automatically.
- At async boundaries, give freshness and completion an explicit owner or resolution protocol. Do not mirror upstream boundary state into local mutable state without explicit ownership and reset semantics. Do not create self-feedback through the same input/update path.
- Remove code made unused by the change. When rule ownership moves or an equivalent execution path appears, remove or disable the old path in the same change when possible. Otherwise provide a staged migration owner and exit condition.
