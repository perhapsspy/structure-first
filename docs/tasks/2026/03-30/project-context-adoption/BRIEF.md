# Goal

이 저장소에 최신 `project-context` 규칙을 실제 런타임 구조와 운영 문서 수준까지 반영한다.

## Scope

- `docs/reference/`와 `docs/tasks/...` 기본 구조 도입
- 저장소용 reference 문서 추가
- 이번 변경을 기록하는 날짜별 task 생성
- `project-context` 설명이 들어가는 외부 문서 정렬
- dogfood playbook/template에서 portable path 및 durable/disposable 경계 정렬

## Current Understanding

- 저장소는 이제 `docs/reference/`와 `docs/tasks/...` 런타임 구조를 갖췄다.
- 외부 문서에서는 `project-context`를 reference notes + dated task records 모델로 소개하도록 맞췄다.
- dogfood 운영 문서는 run artifact를 disposable로 보고, durable 규칙/현재 진행 상태는 reference/task 문서로 보내도록 정렬했다.

## Current State

- 저장소용 `project-context` 운영 기준은 이후 `AGENTS.md`와 설치된 스킬 본문을 canonical source로 정리했다.
- 현재 변경을 위한 날짜별 task 디렉터리와 로그를 만들었다.
- README 한/영 문구와 dogfood 운영 문서를 새 규칙에 맞게 정렬했다.
- `project-context` checker가 현재 runtime shape를 통과했다.

## Next Step

- 후속 write-bearing 작업부터 같은 구조를 계속 사용한다.
- dogfood run에서 반복 규칙이 생기면 task 로그에만 머물지 말고 `docs/reference/`로 승격한다.
- 스킬 계약 자체는 저장소 안에 동명 문서로 복제하지 않고, 프로젝트 고유 차이점만 남긴다.

## Related Docs

- `AGENTS.md`
- `docs/dogfood/README.md`
- `docs/dogfood/templates/structure-first-scale/PIPELINE.md`
- `docs/dogfood/templates/structure-first-scale/STAGE_NOTE.md`

## Working Boundary

- 코드/스킬 동작 로직은 건드리지 않는다.
- 이번 작업은 문서/운영 구조 정렬과 저장소 런타임 shape 도입에 한정한다.

## Latest Validation

- `project-context` checker 실행 결과: `[OK] project-context current runtime shape checks`
