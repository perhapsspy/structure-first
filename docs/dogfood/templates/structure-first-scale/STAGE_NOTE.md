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

같은 run 안의 다른 stage와 같은 agent/worker label을 재사용했다면:

- why same label was reused: `<reason>`

`applier` 단계는 아래 스킬 완료 근거 항목을 덧붙인다:

- `Structural Demand: ... | none; structure unchanged`
- `Readable Behavior: imperative flow | state transition | event lifecycle | rule set | dataflow | protocol interaction | other`
- `Structural Choice: keep | local edit | inline | merge | delete | extract | add boundary; why`
- `Tests: added ... | deferred because ...; next stable responsible unit(s): ...; required contract cases: ...`
- `Decision Ownership: rule -> owner unit; duplicated owner removed? yes/no` when ownership changed
- `Refactor Check: ...` when refactoring work requires it
