# structure-first Scale Dogfood Pipeline

## Goal

현재 scale guidance를 문맥 분리된 멀티 에이전트 단계로 도그푸딩한다.

1. writer가 `structure-first` 영향 없이 `before` 코드를 만든다
2. applier가 각 케이스를 `structure-first`로 개선한다
3. reviewer가 `before/after`를 비교해 finding과 feedback을 뽑는다

여기에 run별 검증 목표를 적는다.

기본 scope:
- 이 run은 `readability/scale-guidance`를 검증한다
- test file이 명시적으로 포함되지 않으면 testing pillar 전체는 검증하지 않는다

## Case Set

- `small-function`: 로컬 함수/파일 하나
- `single-module`: feature module/use case 하나
- `feature-package`: 작은 multi-file capability/subsystem 하나

run 목적에 맞게 케이스 셋을 바꾸거나 교체한다.

## Stage Rules

### 1. Writers

- 읽기 범위:
  - 이 pipeline
  - 자신에게 할당된 `CASE.md` 하나
- 읽지 말 것:
  - `skills/structure-first/**`
  - 모든 `after` 디렉터리
  - 리뷰 산출물
  - 다른 케이스 디렉터리
- 쓰기 범위:
  - 할당된 `before` 파일
  - 할당된 `before/STAGE_NOTE.md`
- 프롬프트 계약:
  - `structure-first`를 언급하지 않는다
  - 저장소 철학에 맞춰 최적화하지 않는다
  - 관습적인 스타일의 그럴듯한 working code를 만든다

### 2. Appliers

- 읽기 범위:
  - 이 pipeline
  - 자신에게 할당된 `CASE.md` 하나
  - 할당된 `before` 파일
  - 할당된 `before/STAGE_NOTE.md`
  - `skills/structure-first/SKILL.md`
- 읽지 말 것:
  - 다른 케이스
  - 리뷰 산출물
- 쓰기 범위:
  - 할당된 `after` 파일
  - 할당된 `after/STAGE_NOTE.md`
- 프롬프트 계약:
  - `structure-first`를 적용한다
  - 수정 전에 현재 작업 단위를 명시한다
  - 그 단위에서 `Primary Flow`가 읽히도록 필요한 만큼만 개선한다

### 3. Reviewers

- 읽기 범위:
  - 이 pipeline
  - case brief
  - 모든 `before/after` 산출물
  - stage note
  - `skills/structure-first/SKILL.md`
  - 회귀 비교가 필요할 때만 이전 run feedback
- 쓰기 범위:
  - `REVIEW.md`
  - `FEEDBACK.md`
- 프롬프트 계약:
  - stage separation, scale handling, outcome quality를 비교한다
  - 항상 issues/risks first로 쓴다
  - 케이스 근거가 충분할 때만 skill 변경을 제안한다

## Context Hygiene Rules

- stage마다 case당 한 에이전트만 쓴다.
- `fork_context=false`를 기본으로 한다.
- write scope는 case와 stage 단위로 분리한다.
- writer와 applier는 각각 `STAGE_NOTE.md`를 남긴다. 항목은 최소 아래를 포함한다:
  - `run root`
  - `agent/worker id`
  - `fork_context`
  - `artifact status` (`fresh` 또는 `reused/copied`)
  - `objective`
  - `files read`
  - `files written`
  - `skill usage`
  - `blockers/compromises`
- artifact를 재사용했다면 source run과 copied path를 적는다.
- reviewer는 stage note를 쓰지 않고, `REVIEW.md`와 `FEEDBACK.md` 안에 근거를 직접 인용한다.

## Expected Artifacts

- `cases/*/CASE.md`
- `cases/*/before/*`
- `cases/*/before/STAGE_NOTE.md`
- `cases/*/after/*`
- `cases/*/after/STAGE_NOTE.md`
- `REVIEW.md`
- `FEEDBACK.md`

## Success Checks

- writer가 `structure-first` vocabulary 없이 plausible baseline 코드를 만들었는가
- applier가 올바른 current unit을 유지한 채 readable `Primary Flow`를 만들었는가
- 큰 케이스가 function-level over-splitting으로 무너지지 않았는가
- 모든 케이스의 test status가 명시적인가 (`added` 또는 `deferred` + next stable Atom(s) + contract cases)
- execution-proof metadata (`agent/worker id`, `fork_context`)가 stage artifact에 보이는가
- review finding이 막연한 취향 차이가 아니라 구체적인 guidance 개선으로 이어지는가
