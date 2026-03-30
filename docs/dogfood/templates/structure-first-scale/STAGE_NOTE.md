# Stage Note

- run root: `<repo-root>/docs/dogfood/runs/<run-name>`
- agent/worker id: `<agent id or worker label>`
- fork_context: `true | false`
- artifact status: `fresh | reused/copied`
- objective: `<이 stage가 만들려던 것>`
- files read:
  - `docs/dogfood/runs/<run-name>/cases/<case-name>/CASE.md`
- files written:
  - `docs/dogfood/runs/<run-name>/cases/<case-name>/<stage>/STAGE_NOTE.md`
- skill usage:
  - `<none | skill path and how it was used>`
- blockers/compromises:
  - `<compromise 1>`

재사용/복사한 경우:

- source run: `<repo-root>/docs/dogfood/runs/<source-run-name>`
- copied into:
  - `docs/dogfood/runs/<run-name>/cases/<case-name>/<stage>/...`

applier stage는 아래 skill completion evidence 줄을 덧붙인다:

- `Current Unit: ...`
- `Primary Flow: ...`
- `Boundaries: ...`
- `Tests: added ... | deferred because ...; next stable Atom(s): ...; required contract cases: ...`
- `Decision Ownership: rule -> owner unit; duplicated owner removed? yes/no` when ownership changed
- `Refactor Check: ...` when refactoring work requires it
