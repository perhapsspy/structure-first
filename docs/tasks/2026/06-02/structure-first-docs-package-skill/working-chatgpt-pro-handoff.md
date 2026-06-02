# Structure-first-docs package skill handoff

## Question

How should `structure-first-docs` evolve from a single-document restructuring/review skill into a skill for composing and reviewing engineering document packages that prepare good code work?

## Current Skill Gap

The old skill handled source fidelity, tentative language, minimal sections, and issue-first review for one document. It did not explicitly teach an agent to review a multi-file package for:

- entrypoint quality
- reader routes
- canonical ownership per topic
- evidence/history/draft/archive separation
- duplicate current conclusions
- gate/runbook completeness
- package growth caused by unresolved ownership

## Observed Examples

### Example 1: Router-heavy system-design package

This package is a large Edge Agent system-design task root. It has many root-level documents, but the package is still navigable because it has a strong router and explicit ownership table.

The entrypoint says the package owns the Edge Agent managed replacement proposal and pre-implementation contracts. It tells readers to start with:

1. `BRIEF.md` for compact resume state and the next step.
2. non-live baseline review for the scope closed without a real Edge.
3. Docker fake Edge pre-canary for the lifecycle and observability scenario closed before real Edge work.
4. payload canary freeze packet for the target/release/rollback/actor/memo record before one-device canary.
5. backlog for remaining gates and the next host-probe decision.
6. live readiness packet, live/fleet gates, host access recovery, and reference validation stages for actual Edge readiness.

The same entrypoint then separates "what to read first" from "which document owns which topic." It says proposal owns the top-level actor relationship and recommendation, implementation spec owns requirement IDs and acceptance criteria, control plane owns the work lease/report API and storage boundary, signal-control contract owns event/metric/heartbeat/current/result payloads and contract tests, lifecycle contract owns ingress/update/recovery behavior, implementation plan owns sequence and gates, readiness owns pre-implementation gates, and live/fleet gate owns live-only restart conditions.

This is a good package pattern because `README.md` is not trying to restate all current truth. It routes. `BRIEF.md` is not trying to be the whole design. It resumes. Root-level topic docs are allowed to be substantial because each one owns a distinct current concern.

Risk revealed by this example: a package can have many files and still be good, so the skill must not judge package quality by file count. It should judge whether the files have distinct ownership and a readable route.

### Example 2: Migration/demotion package

This package is an older `ops-infra` Edge management task whose design ownership moved to a newer `edge-agent-workspace` package.

Its entrypoint does not pretend to remain the design source of truth. It says the design canonical source moved to the new workspace task root. The old `ops-infra` task keeps only pre-migration investigation records, live operation evidence, and append-only logs.

It explicitly says it still owns:

- live deploy, Slack, Edge access, and operations evidence
- operation-state rechecks
- pre-move research and append-only logs

It explicitly says it no longer owns:

- Edge Agent system-design canon
- new `edge-ops` protocol/API/fixture canon
- implementation cards and repo-specific validation commands

A former canonical file such as the control-plane document has been demoted into a pointer. It says the control-plane canon moved to the new workspace, and new protocol/API/fixture changes should happen there; `ops-infra` should only update live deploy state and operations evidence.

This is a good migration pattern because old files do not compete with the new owner. They either route to the new owner or preserve historical/live evidence.

Risk revealed by this example: package review needs an explicit migration/demotion check. If ownership moved, old root docs must not still read like active canonical modules unless they clearly say they are historical or routing stubs.

### Example 3: Topic-rich implementation package

This package is a Backoffice fieldwork task root. It combines product model, contracts, UI surfaces, system boundaries, deployment, validation, and implementation follow-through.

Its `BRIEF.md` works as a current resume card. It states the goal, scope, current facts, current state, next step, and a compact working boundary. It does not paste command logs. It summarizes deployment and validation status in current-state language.

The model document is a strong canonical module. It opens by saying exactly what it owns: fieldwork-data owners, relationships, and minimum fields. It then points adjacent ownership elsewhere:

- type-level contracts belong to `CONTRACTS.md`
- creation order and example flows belong to `EXECUTION.md`
- system boundaries and permission interpretation belong to `SYSTEM_BOUNDARIES.md`
- outbox delivery adoption belongs to an adoption note

That is useful because the model doc explains its own boundary before giving details. The package does not force every topic into one giant document.

The pages subtree also has a router. It says `WORKSPACE_COMPOSITION.md` owns the shared workspace spine, `shared/` owns surfaces reused across services, `backoffice/` owns Backoffice composition, and `patch/` owns Patch composition.

The `working/README.md` is another useful pattern. It says `working/` contains dormant notes that do not conflict with current implementation, and that intermediate outputs already absorbed into canonical docs or references should not be preserved there.

Risk revealed by this example: topic-rich packages benefit from local owner declarations inside canonical documents, not just a top-level router.

### Example 4: Ambiguous backlog surface

The fieldwork implementation backlog shows why backlog style must be explicit.

It says the document owns "implementation items to continue," but the body mixes several kinds of material:

- many completed checked items
- a few still-open items
- deployment preparation
- validation commands
- staging questions
- browser smoke status
- follow-up component-splitting ideas

This may be acceptable if the backlog is intentionally a live checklist with completed evidence retained. It would be bad if readers expect completed items to disappear after worklog capture, or if the backlog has quietly become a historical audit document.

Risk revealed by this example: a skill should not blindly delete or rewrite a backlog. It should first ask what backlog style is intended: live checklist, deletion-style TODO, or historical audit. That decision may be parent-owned.

## Working Thesis

Good document packages are like good code packages:

- one clear entrypoint
- small modules with single responsibility
- explicit dependencies and reading order
- one owner for each current contract, decision, gate, or plan
- evidence and history kept out of current-state modules
- stale material preserved only when clearly marked as stale

The target skill should not define a storage layout. Repositories may already have their own task roots, archive rules, logs, references, or handoff conventions. `structure-first-docs` should own semantic package quality and reader flow.

## Proposed Skill Shape

Modes:

- Document Compose
- Document Review
- Package Compose
- Package Review

Package ownership lens:

- entrypoint
- router
- canonical module
- gate packet
- backlog/TODO
- evidence/research
- working note
- log
- archive
- reference candidate

Review checklist:

- Missing or misleading entrypoint
- No reader path for resume, decision, implementation, verification, or operation
- Duplicate owners for the same current decision, contract, gate, or plan
- Root-level drafts/evidence/stale reports pretending to be current
- Current-state summaries polluted by chronology or command transcripts
- Logs/research containing the only current conclusion
- Backlog style ambiguity: live checklist, deletion-style TODO, or historical audit
- Gate/runbook docs missing preconditions, stop conditions, rollback, evidence, or approval boundary
- Migration/demotion ambiguity after ownership moved
- Links to archived/stale material without status labels
- Parent-owned decisions such as canonical-vs-router status, reference promotion, archive retention
- Package size caused by ownership ambiguity rather than useful modularity

## Open Questions for External Review

- Is the package ownership model too specific to project-context, or general enough for engineering docs broadly?
- Should the skill include stronger instructions for when to split a document versus keep it as one file?
- Should package compose include a named "foundation packet" archetype for future code work, or would that become a forced template?
- Are gate packets and runbooks distinct enough to keep as separate concepts?
- What examples would best test whether the skill improves real agent output?

## External Review Feedback Applied

The final direction should be shorter and more independent than the first draft:

- remove references to any specific companion skill
- avoid making one repository's path layout look universal
- prefer durable principles and output contracts over long procedural checklists
- keep package roles concise
- treat the Korean file as a review companion, not the canonical skill source
