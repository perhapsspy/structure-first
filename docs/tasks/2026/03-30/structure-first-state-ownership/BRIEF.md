# Goal

`structure-first` 스킬 본문에 상태 write owner, self-feedback/mirror sync 금지, async freshness/completion contract를 프레임워크 중립 규칙으로 반영한다.

## Scope

- `skills/structure-first/SKILL.md` 영문 본문 수정
- `skills/structure-first/SKILL.ko.md` 의미 동기화
- core skill 메시지를 유지한 채 일반 구조 규칙만 보강
- 이번 변경을 날짜별 task로 기록

## Current Understanding

- backoffice의 반복 반응성 사고는 Svelte 문법보다 `상태 소유자 분산`, `self-feedback`, `최신성/완료 계약 부재`가 공통 원인이다.
- 이 패턴은 특정 프레임워크 팁이 아니라 `structure-first`의 `decision owner`, `single composition point`, `contract-driven tests`를 상태/비동기 경계까지 확장하는 문제로 해석할 수 있다.
- core skill 본문에는 `$effect`, patchmap, renderer 같은 제품/프레임워크 고유 표현을 넣지 않는 편이 맞다.

## Current State

- 영문/국문 스킬 본문에 상태 write owner, mirror sync 금지, async boundary contract 보강 문구를 반영했다.
- `single commit point`나 성능 전술은 별도 대원칙으로 올리지 않고 기존 ownership/composition 규칙에 흡수하거나 제외했다.
- 이번 변경용 task 문서를 추가했다.

## Next Step

- 필요하면 이후 examples나 내부 메모에서 프런트엔드 사례를 별도로 풀되, core skill 본문은 일반 원칙으로 유지한다.
- 다음 dogfood에서 이 보강 문구가 실제 코드 리뷰/리팩터링 지시 품질을 높이는지 본다.

## Related Docs

- `skills/structure-first/SKILL.md`
- `skills/structure-first/SKILL.ko.md`
- `docs/INSIGHTS.md`
- `docs/ORIGIN.md`

## Working Boundary

- public README, examples, docs skill은 건드리지 않는다.
- 이번 작업은 core skill wording 보강에 한정한다.

## Latest Validation

- `git diff --check`로 문법/공백 이상 여부를 확인한다.

