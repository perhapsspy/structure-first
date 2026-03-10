---
name: structure-first-docs
description: Restructure and review engineering documents with source-fidelity-first rules. Preserve original meaning and useful source form, avoid adding new facts or forced decisions, and keep issue/risk-first feedback. Use for design docs, refactor plans, migration plans, PR narratives, and runbooks.
license: MIT
metadata:
  author: perhapsspy@gmail.com
  version: '1.0'
  source_repository: https://github.com/perhapsspy/structure-first
---

# Skill: Structure First Docs

## Purpose

Restructure and review engineering documents so readers can follow the content in one top-down pass.
Preserve source meaning first. Do not invent facts. Do not finalize decisions that were not finalized in the source.
Preserve useful source form too. Do not flatten emails, checklists, ADRs, or handoff notes into one generic output shape unless readability clearly improves.

## Modes

1. **Compose**
- Draft/rewrite documents in readable top-down flow.

2. **Review**
- Review documents and return issues/risks first.

## When to Use

- Design docs, refactor/migration plans, runbooks, PR narratives
- Technical doc review before implementation/share

## Do Not Use

- Marketing/brand copy
- Strict compliance/legal content owned by policy/legal teams

## Core Rules

1. Fix intent in one sentence first.
2. Build `Primary Reader Flow` from existing source content.
3. `Source fidelity first`: every statement must be traceable to source text.
4. Do not add new facts, constraints, metrics, owners, dates, or policy values unless explicitly provided.
5. Do not upgrade tentative language into confirmed decisions.
6. Preserve tentative wording strength. `might`, `seems`, `looks like`, `likely`, `maybe`, and similar language should stay at similar strength.
7. If chronology is part of the meaning (timestamps, incident sequence, handoff order), preserve that chronology unless reordering clearly improves readability without losing meaning.
8. If information is missing, keep it as `Open Questions` or `Unknown`, not assumptions.
9. Preserve source form when it is already useful. Emails should still feel like emails; checklists should still feel like checklists.
10. Prefer exact no-op when readability gain is marginal. Do not edit just to show structure.
11. In review mode, always start with issues/risks.
12. Review should clarify document state/scope/risk. Do not redesign the underlying system unless the source already frames that redesign.

## Compose Structure (Adaptive)

Do not force a fixed template.
Prefer source-native form first.

Use minimum sections first:
- `Intent`
- `Current Facts`
- `Next Actions`

Add sections only when needed:
- `Decisions` (only confirmed decisions from source)
- `Risks`
- `Open Questions`
- `Appendix`

If the source is already readable enough:
- prefer exact no-op,
- keep the original format,
- or make only light-touch reordering/label cleanup.

## Review Structure

- Start with `Issues/Risks` (severity-ordered).
- Then provide `Evidence` and `Required Changes`.
- Keep `Open Questions/Assumptions` only if needed.
- Add a brief summary only when requested.
- Prefer requests for clarification, scoping, or status labeling over proposing a new design.

## Execution Steps

1. Identify mode (`Compose` or `Review`).
2. Identify the source form (email, checklist, ADR, handoff, memo, etc.).
3. Extract source units: facts, decisions, actions, unknowns.
4. Detect whether chronology itself carries meaning.
5. Reorder only as much as needed for readable top-down flow.
6. Keep source-native form when it already works; use adaptive sections only when they help.
7. Prefer exact no-op when the gain is negligible.
8. Verify each statement is source-traceable.
9. Verify tentative wording was not strengthened.
10. Convert missing or uncertain items into explicit questions.
11. Keep output concrete and non-speculative.
12. If direct edit is possible, edit target files directly.
13. If direct edit is blocked, return publish-ready Markdown with failure reason.

## Final Checks

- Can a reader understand the decision path in one top-down pass?
- Did any new fact get added that is not in source?
- Did any tentative idea become a confirmed decision?
- Did tentative wording stay at similar strength?
- If chronology mattered, was it preserved?
- Did the output preserve useful source form instead of flattening it?
- Are sections minimal for this document?
- Would exact no-op or lighter touch have been better?
- In review mode, are issues/risks first?
- In review mode, did the response avoid drifting into redesign?
