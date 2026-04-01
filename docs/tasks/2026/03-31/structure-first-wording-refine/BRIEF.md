# Goal

리뷰에서 지적된 과도한 frontend-specific wording과 문서 정렬 문제를 줄이도록 `structure-first` core skill 문구를 축소 수정한다.

## Scope

- `skills/structure-first/SKILL.md` 문구 다듬기
- `skills/structure-first/SKILL.ko.md` 의미 동기화
- 리뷰와 서브에이전트 브레인스토밍 결과 반영
- core skill 본문 범위는 유지하고 wording만 조정

## Current Understanding

- 추가한 방향 자체는 맞지만, 현 문구는 core public skill 치고는 프런트엔드 상태관리 사례에 너무 가깝다.
- 공통 리뷰 포인트는 세 가지였다: anti-pattern 문장 일반화, async contract와 strategy 분리, 새 개념/새 gate와 문서 나머지 정렬 개선.
- 가장 작은 수정은 `props/stores`류 표현 제거, async 문장 축소, `Meaning state`와 `Final Gate` 부담 완화다.

## Current State

- 영문/국문 스킬 페어에서 프런트엔드 고유 표현을 일반화했다.
- async 문장은 strategy 예시를 걷어내고 freshness/completion contract 중심으로 줄였다.
- ownership 문구는 기존 `Equivalent path`와 더 잘 맞도록 `externally observable result` 축으로 정렬했다.
- `Completion Evidence`의 `Tests` 줄에 관련 contract를 적을 수 있게 보강했다.
- `single-writer` 문장은 default bias로 낮추고, multi-writer coordination이 책임인 경우 coordinator를 명시하라고 정리했다.
- `mirror-sync`와 `self-feedback` 문장은 비교 단위와 허용 조건이 더 직접 읽히도록 다듬었다.

## Next Step

- 필요하면 다음 리뷰에서 한국어 문장의 리듬과 용어 밀도를 한 번 더 다듬는다.
- 이후 dogfood에서 이 wording이 실제로 더 범용적으로 작동하는지 확인한다.
- 문구 루프는 이번 정렬 확인까지 마치고, 그 다음부터는 실제 dogfood 결과로 판단한다.

## Related Docs

- `skills/structure-first/SKILL.md`
- `skills/structure-first/SKILL.ko.md`
- `docs/tasks/2026/03-30/structure-first-state-ownership/BRIEF.md`

## Working Boundary

- README/examples/other skills는 건드리지 않는다.
- 이번 작업은 review findings를 줄이기 위한 wording refine에 한정한다.

## Latest Validation

- `git diff --check` 통과
- `project-context` checker 결과: `[OK] project-context current runtime shape checks`
