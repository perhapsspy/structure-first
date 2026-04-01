# Goal

dogfood playbook의 provenance 규칙을 강화하고, 실제 서로 다른 subagent를 써서 `structure-first` wording dogfood를 다시 실행한다.

## Scope

- `docs/dogfood/README.md`와 `structure-first-scale` template에 stage separation 규칙 보강
- 새 rerun용 dogfood run 생성
- writer/applier/reviewer를 실제 서로 다른 subagent로 실행
- 이번 rerun 작업을 날짜별 task로 기록

## Current Understanding

- 기존 `structure-first-wording-20260401` run은 synthetic evidence는 만들었지만, 같은 메인 에이전트가 모든 stage를 작성해 provenance가 약했다.
- 이 문제는 skill wording보다 pipeline rule과 실제 실행 방식에 더 가깝다.
- rerun에서는 메인 에이전트가 scaffold/orchestration만 맡고, `before/after/REVIEW/FEEDBACK`은 subagent가 써야 한다.

## Current State

- playbook/template에 distinct subagent 규칙을 추가했다.
- `structure-first-wording-rerun-20260401` run을 만들고 case brief를 복사했다.
- writer 3명, applier 3명, reviewer 1명을 실제 서로 다른 subagent로 실행해 `before/after/REVIEW/FEEDBACK`을 채웠다.
- reviewer 결과, provenance 문제는 해결됐고 남은 owner는 `pipeline`(test-bearing case 부족)과 `artifact`(backend/event-driven case 부재, small-function contract gap)로 좁혀졌다.

## Next Step

- 다음 dogfood에서는 test-bearing stage 또는 case를 추가해 contract claims를 실제로 검증한다.
- backend/event-driven coordinated writer 케이스를 추가해 wording coverage를 넓힌다.
- `small-function-sync-loop` artifact는 no-op contract를 맞추거나 CASE/feedback wording을 더 정확히 맞춘다.

## Related Docs

- `docs/dogfood/README.md`
- `docs/dogfood/templates/structure-first-scale/PIPELINE.md`
- `docs/tasks/2026/04-01/structure-first-wording-dogfood/BRIEF.md`

## Working Boundary

- 이번 작업은 dogfood pipeline 개선과 rerun evidence 생성에 한정한다.
- 기존 run은 historical disposable artifact로 남겨두고, rerun을 새 run으로 만든다.

## Latest Validation

- playbook/template diff 확인
- rerun artifact 구조 확인
- `git diff --check`
- `project-context` checker 결과: `[OK] project-context current runtime shape checks`
