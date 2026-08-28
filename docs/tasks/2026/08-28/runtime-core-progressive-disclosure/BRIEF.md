# Goal

`structure-first`의 현재 의미와 적용 범위는 유지하면서 실행 시 핵심 판단을 더 짧고 선명하게 전달하고, 조건부 세부 규칙은 필요한 작업에서만 읽게 한다.

## Scope

- `SKILL.md`와 `SKILL.ko.md`를 runtime contract와 명시적 reference routing 중심으로 재구성한다.
- ownership·async·representation·migration과 verification 세부 규칙을 한·영 reference pair로 옮긴다.
- 기존 description, invocation policy, 제품 bundle, release는 바꾸지 않는다.
- 모호한 owner와 completion 사례에서 현재 정본과 후보를 A/B 검증한다.

## Current Understanding

- 이전 A/B에서 전체 규칙보다 177-word runtime core가 root-cause owner 선택을 더 안정적으로 유도했고 실행 시간과 출력량도 줄였다.
- 후보의 목적은 규칙 삭제가 아니라 runtime salience 개선이다.
- main skill은 작업 중 항상 필요한 owner·flow·smallest unit·observable contract를 보유하고, 세부 경계 규칙은 적용 조건과 함께 한 단계 아래에서 읽힌다.

## Current State

- 사용자 리뷰를 반영한 한·영 문서 구조를 정본 저장소 working tree에 구현하고 package·link·project-context 검증을 통과했다.
- 새 owner/completion 사례에서는 현재 전체, 후보 main, 후보 routed가 모두 8/8 계약을 만족했다.
- 기존 판별 root-cause 사례에서는 현재 전체 2/4, 후보 main 4/4, 후보 routed 3/4였다. 후보는 회귀 없이 핵심 owner 선택을 개선했지만 reference를 불필요하게 선주입하면 일부 희석됐다.
- 실행 시간과 token은 표본·cache 편차가 커서 후보의 효율 개선 근거로 사용하지 않는다.
- 사용자가 canonical 반영과 Project Legibility 동기화를 승인했다. plugin release는 이 작업에 포함하지 않는다.

## Next Step

- canonical `main`에 commit·push하고 확정 SHA로 Project Legibility bundle과 lock을 동기화한다.

## Working Boundary

- `skills/structure-first/`
- `docs/tasks/2026/08-28/runtime-core-progressive-disclosure/`
