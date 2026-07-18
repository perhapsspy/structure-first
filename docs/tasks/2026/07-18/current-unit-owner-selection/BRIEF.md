# Goal

`structure-first`가 증상이나 결과가 보이는 위치가 아니라 바꾸려는 동작이나 규칙의 실제 책임을 기준으로 가장 작은 current unit을 고르게 한다.

## Scope

- `SKILL.md` 한·영 pair의 범용 current-unit 선정 원칙만 보강한다.
- canonical `main`에 검증된 변경을 공개하고 Project Legibility의 downstream release로 연결한다.
- trigger, 공개 metadata와 README는 변경하지 않는다.

## Current Understanding

- 증상 위치, current unit, change boundary와 verification scope는 서로 같지 않을 수 있다.
- `smallest`와 `responsible`을 함께 두면 실제 owner를 찾으면서도 국소 버그를 subsystem 작업으로 키우지 않는다.
- `lifetime`이나 `coordination scope` 같은 사례 유래 용어보다 behavior/rule responsibility가 언어와 실행 모델에 덜 편향된다.

## Current State

- 한·영 Operating Model 첫 문장을 같은 의미로 교체했다.
- 세 관점의 독립 사전 리뷰, backend·systems·pure parser forward-test, 세 관점의 최종 diff 리뷰가 범용성과 국소성 보존을 확인했다.
- skill validator, diff check와 project-context shape check가 통과했다.
- canonical `main`에 공개된 source를 Project Legibility가 고정할 준비가 됐다.

## Next Step

- Project Legibility contribution 절차에서 canonical commit을 고정하고 patch release로 배포한다.

## Working Boundary

- `skills/structure-first/SKILL.md`
- `skills/structure-first/SKILL.ko.md`
- `docs/tasks/2026/07-18/current-unit-owner-selection/`
