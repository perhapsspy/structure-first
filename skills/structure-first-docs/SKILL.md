---
name: structure-first-docs
description: Compose, clean up, restructure, audit, and review project docs and documentation packages for source-of-truth ownership, current-vs-stale cleanup, reader routes, task docs, handoffs, design docs, implementation plans, migration plans, runbooks, PR narratives, backlog/log/evidence separation, and implementation readiness.
license: MIT
metadata:
  author: perhapsspy@gmail.com
  version: '1.0'
  source_repository: https://github.com/perhapsspy/structure-first
---

# Skill: Structure First Docs

## Purpose

Make project documents and document packages easy to read, resume, review, and use as a basis for code work.

For large efforts, treat the document set like a code package: clear entrypoint, small modules with one responsibility, explicit reader routes, and separate places for current source of truth, evidence, history, drafts, and stale material.

## Modes

- **Document Compose**: draft or rewrite one document.
- **Document Review**: review one document; lead with issues and risks.
- **Package Compose**: build or restructure a multi-file design, migration, runbook, implementation, or handoff package.
- **Package Review**: review a package for ownership, navigation, stale state, duplication, and implementation readiness.

## Principles

- Follow existing repository or workspace conventions for paths, filenames, logs, archives, and work areas. This skill defines semantic document quality, not storage layout.
- Preserve source meaning. Do not invent facts, commitments, owners, dates, metrics, constraints, or decisions.
- Keep tentative language tentative. Do not turn possibilities, suspicions, or options into decisions.
- Separate current source of truth from evidence, chronology, drafts, and archived material.
- One current decision, contract, gate, or plan should have one owning document.
- A package entry document should usually be current canon, a router, or a bounded execution/runbook packet.
- Preserve useful source form. Emails, checklists, ADRs, runbooks, handoffs, and logs should keep their native shape when that shape is useful.
- Prefer no-op or light-touch edits when structure would not materially improve.
- Reviews clarify document state, ownership, scope, and risk. Do not redesign the underlying system unless the source already frames that redesign.

## Package Roles

Use these roles as a lens, not a required template:

- **Entrypoint**: states package purpose, current state, and where to start.
- **Router**: maps reader goals to documents and names each file's responsibility.
- **Canonical module**: owns one current topic, contract, model, decision, or plan.
- **Gate/runbook**: owns preconditions, allowed actions, stop conditions, owner/approval boundary, evidence, rollback, and recovery.
- **Backlog/TODO**: makes its style explicit: live checklist, deletion-style TODO, or historical audit.
- **Evidence/log**: preserves proof and chronology without pretending to be current canon.
- **Working/archive**: keeps undecided or stale material separate from current documents.
- **Reference candidate**: contains reusable current context that may deserve promotion to a durable reference area.

## Compose Rules

Start from reader jobs, not from a fixed template:

- **Resume**: what is true now, what is next, and what is blocked?
- **Decide**: what facts, options, tradeoffs, and open questions matter?
- **Implement**: what contracts, boundaries, sequence, and acceptance criteria guide code work?
- **Verify**: what gates, commands, scenarios, and evidence close the work?
- **Operate**: what runbook, rollback, owner, and stop conditions matter?

Create only the surfaces the source justifies. If two documents repeat the same current conclusion, choose one owner when the source or existing convention makes ownership clear; otherwise flag an ownership decision.

For migrations or moved ownership, make demotion explicit: old files should route to the new owner or state historical/archive status, not compete as canon.

When an existing surface already owns a fact, decision, or route, edit that surface before adding explanatory prose elsewhere.
Treat user corrections and deletion requests as edit inputs: replace, delete, demote to archive/working, or point to the owning surface.
Do not preserve removed material as warnings, defensive rationale, unsupported audience assumptions, or duplicate routes in current documents.

## Review Rules

Start with `Issues/Risks`, ordered by severity. Then give evidence and required changes.

Look for:

- missing or misleading entrypoint
- unclear reader path for resume, decision, implementation, verification, or operation
- duplicate owners for the same current decision, contract, gate, or plan
- drafts, evidence dumps, or stale reports that look current
- current summaries polluted by chronology or command transcripts
- logs or research that contain the only current conclusion
- backlog style ambiguity or mixed open/completed/deployment/validation/staging material
- gate/runbook docs missing preconditions, stop conditions, rollback, recovery, evidence, or approval boundary
- migration packages where old files still look canonical after ownership moved
- links to stale or archived material without status labels
- decisions requiring explicit ownership or policy choice, such as canonical-vs-router status, reference promotion, archive retention, or backlog style

If a change requires an ownership or policy choice not settled by the source, label it as a decision request instead of silently rewriting.
Do not rewrite append-only logs just to make them neater; sample relevant tails unless historical cleanup is explicitly requested.

## Output Contract

For compose work, edit directly when possible; otherwise return publish-ready Markdown and name any blocked inputs.

For review work, use this shape:

```text
Issues/Risks
Evidence
Required Changes
Open Questions or Decision Requests
```
