# Structure First - Pre-Skill Insights
> Note: This English text was translated and edited with LLM assistance. If anything reads awkwardly, please check the Korean version or open an issue.

This document records coding habits and structural instincts that were organized before `structure-first` became a formal skill.
It is intended to be a baseline for future derivative skills such as `structure-first-docs`.

[Korean Original](INSIGHTS.md) | [English](INSIGHTS.en.md)

## 1) Read Order and Flow

- Put the most important/external-facing part first.
- Reading top-down should naturally go from `Primary Flow -> details`.
- Keep branches/exceptions from breaking the main flow (early return or lower placement).

## 2) Decomposition Sense (Function/Module Splitting)

- Splitting is not the goal. Split only when readability improves.
- Avoid over-splitting functions/files that creates utility sprawl.
- Split only where responsibility or boundary actually changes.

## 3) Composability (Reuse Style)

- Prefer composable primitive sets over broad generic utility helpers.
- Keep primitives with clear I/O; prefer pure functions when possible.
- Move key generation/policies outward to improve composability and flexibility.

## 4) State/Context Stance

- Reduce class/`this` dependence; prefer pure-function style.
- Gather side effects at boundaries (orchestrator/I/O); keep inner logic focused on computation/decisions.
- Handle cache/global state with explicit policy and boundary ownership.

## 5) Naming Sense

- Avoid abbreviation-heavy naming; keep names short with stable meaning in context.
- Prefer verb-based names that immediately reveal action.
- If names become sentence-like, treat it as a structural warning signal.

## 6) Code Density/Formatting (Readability Rule)

- Minimize unnecessary line breaks; keep one-line expressions one-line when readable.
- Allow multiline `const` groups only when several values are handled together.
- Use ternary expressions when readability is preserved.
- Keep refactoring diffs minimal when possible; avoid full rewrites by default.

## 7) Test Philosophy (Atom-Level + Test Readability)

- If code is decomposed into atoms, add sufficient unit tests at atom level.
- Focus on contracts (`input -> output`, invariants, edge cases), not implementation-following behavior.
- Keep test code readable as first-class code.
  - Use `each`/table cases to reduce repetition.
  - Use small helpers/factories when they clarify intent, but avoid helper sprawl.
  - Keep one test focused on one core assertion.
  - Use case names to preserve context in test data.

## Mid Summary: Working Memo That Compressed Insights Into a Skill

- Fix intent first: write the change goal in one sentence.
- Build readable success flow first: make it readable in one top-down pass.
- Define minimal boundaries: classify I/O, decision, transform without boundary inflation.
- Splitting is a means, not an end: split only when readability improves.
- Atoms must keep fixed roles: clear I/O and pure function preference.
- Keep composition ownership in one place: orchestrator-centric composition, fewer direct atom-to-atom dependencies.
- Push side effects to boundaries: keep inner logic focused on computation/decision.
- Achieve reuse through composition: avoid speculative abstractions.
- Write sufficient atom-level tests: validate contracts, not internals.
- Keep test code readable: table cases plus restrained helper usage.

## Extension Hints for `structure-first-docs`

- Prefer short rules + execution order + checklist over long convention prose.
- Apply `Primary Reader Flow` to documents too, without forcing a fixed template.
- Treat `Intent -> Decision -> Steps -> Risks -> Open Questions` as a commonly useful default flow example.
- Keep "issues/risks first" as the default contract for review responses.
