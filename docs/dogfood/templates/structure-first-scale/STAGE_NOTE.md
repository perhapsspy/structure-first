# Stage Note

- run root: `<absolute run root>`
- agent/worker id: `<agent id or worker label>`
- fork_context: `true | false`
- artifact status: `fresh | reused/copied`
- objective: `<이 stage가 만들려던 것>`
- files read:
  - `<absolute path>`
- files written:
  - `<absolute path>`
- skill usage:
  - `<none | skill path and how it was used>`
- blockers/compromises:
  - `<compromise 1>`

재사용/복사한 경우:

- source run: `<absolute path>`
- copied into:
  - `<absolute path>`

applier stage는 아래 skill completion evidence 줄을 덧붙인다:

- `Current Unit: ...`
- `Primary Flow: ...`
- `Boundaries: ...`
- `Tests: added ... | deferred because ...; next stable Atom(s): ...; required contract cases: ...`
- `Decision Ownership: rule -> owner unit; duplicated owner removed? yes/no` when ownership changed
- `Refactor Check: ...` when refactoring work requires it
