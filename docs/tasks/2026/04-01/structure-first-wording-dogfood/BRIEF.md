# Goal

최근 `structure-first` wording refinement가 실제 코드 생성/개선에서 과도하게 적용되지 않는지 dogfood run으로 검증한다.

## Scope

- `docs/dogfood/runs/structure-first-wording-20260401/` run 생성
- wording 리스크를 겨냥한 case set 작성
- 이번 dogfood 준비 작업을 날짜별 task로 기록
- stage 실행 전에 검증 포인트를 명확히 고정

## Current Understanding

- 최근 wording loop로 `frontend-specific wording`, `latest-wins` 뉘앙스, `single-writer` 절대 규칙 문제가 많이 줄었다.
- 남은 검증 포인트는 `single-writer bias`, `mirror-sync/local adaptation`, `async freshness conflict`가 실제 stage 산출물에서 어떻게 읽히는지다.
- 현재 단계에서는 run scaffold와 case brief를 먼저 만드는 것이 맞고, writer/applier/reviewer 실행은 그다음 단계다.

## Current State

- `structure-first-wording-20260401` run을 만들었다.
- pipeline과 review/feedback 템플릿, 3개 case brief를 채웠다.
- 3개 케이스의 `before/after` artifact와 stage note를 모두 작성했다.
- reviewer 결과, wording 자체보다 provenance와 coverage가 다음 owner라는 결론을 얻었다.
- 이번 작업용 task 문서를 추가했다.

## Next Step

- 다음 run에서는 실제 서로 다른 에이전트로 stage를 분리해 provenance를 강화한다.
- backend/event-driven coordinated writer 케이스를 추가해 coverage를 넓힌다.

## Related Docs

- `docs/dogfood/README.md`
- `docs/dogfood/runs/structure-first-wording-20260401/PIPELINE.md`
- `docs/tasks/2026/03-31/structure-first-wording-refine/BRIEF.md`

## Working Boundary

- 이번 작업은 synthetic dogfood run 1회를 끝까지 수행하는 데 한정한다.
- run evidence를 바탕으로 owner를 `pipeline / coverage` 쪽으로 분류한다.

## Latest Validation

- run artifact 구조가 playbook/template와 맞는지 다시 읽어 확인한다.
- `git diff --check`
- `project-context` checker 결과: `[OK] project-context current runtime shape checks`
