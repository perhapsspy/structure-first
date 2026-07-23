# structure-first 규모별 도그푸딩 절차

## 목표

현재 구조 탐색 지침을 서로 문맥이 분리된 여러 에이전트 단계로 검증한다.

1. `writer`가 `structure-first` 영향 없이 `before` 코드를 만든다
2. `applier`가 각 사례를 `structure-first`로 개선한다
3. `reviewer`가 `before/after`를 비교해 발견한 문제와 개선 의견을 뽑는다

여기에 실행별 검증 목표를 적는다.

기본 범위:
- 이 실행은 읽기 쉬움과 규모별 지침을 검증한다
- 테스트 파일이 명시적으로 포함되지 않으면 테스트 지침 전체는 검증하지 않는다

## 사례 묶음

- `small-function`: 로컬 함수/파일 하나
- `single-module`: 기능 모듈이나 유스케이스 하나
- `feature-package`: 여러 파일로 이루어진 작은 기능 묶음이나 하위 체계 하나

실행 목적에 맞게 사례 묶음을 바꾸거나 교체한다.

## 단계 규칙

### 1. Writers(초안 작성자)

- 읽기 범위:
  - 이 실행 절차
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
  - 관습적인 스타일의 그럴듯하게 동작하는 코드를 만든다
  - 전담 `writer` 하위 에이전트 하나가 사례 하나만 맡는다

### 2. Appliers(적용자)

- 읽기 범위:
  - 이 실행 절차
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
  - 구조를 읽고 추적하기 어려운 구체적인 문제와 자연스러운 읽기 형태를 확인한다
  - 기존 구조 유지, 국소 변경, 변경하지 않음을 포함해 필요한 만큼만 개선한다
  - `writer`와 다른 전담 `applier` 하위 에이전트가 사례 하나만 맡는다

### 3. Reviewers(검토자)

- 읽기 범위:
  - 이 실행 절차
  - 사례 설명
  - 모든 `before/after` 산출물
  - 단계 기록
  - `skills/structure-first/SKILL.md`
  - 회귀 비교가 필요할 때만 이전 실행의 개선 의견
- 쓰기 범위:
  - `REVIEW.md`
  - `FEEDBACK.md`
- 프롬프트 계약:
  - 단계 분리, 규모별 대응과 결과 품질을 비교한다
  - 항상 문제와 위험을 먼저 쓴다
  - 사례 근거가 충분할 때만 스킬 변경을 제안한다
  - `reviewer` 하위 에이전트는 어떤 `writer`나 `applier`와도 다른 표지를 사용한다

## 문맥 분리 규칙

- 단계마다 사례당 한 에이전트만 쓴다.
- `fork_context=false`를 기본으로 한다.
- 같은 사례에서 `writer`와 `applier`에 같은 `agent/worker label`을 재사용하지 않는다.
- `reviewer`는 `writer`·`applier`와 다른 `agent/worker label`이어야 한다.
- 메인 에이전트는 실행 틀과 단계 조정까지만 맡고, 실행 산출물(`before/after/REVIEW/FEEDBACK`) 작성은 하위 에이전트에 위임하는 것을 기본으로 한다.
- 쓰기 범위는 사례와 단계 단위로 분리한다.
- `writer`와 `applier`는 각각 `STAGE_NOTE.md`를 남긴다. 항목은 최소 아래를 포함한다:
  - `run root`
  - `agent/worker id`
  - `fork_context`
  - `artifact status` (`fresh` 또는 `reused/copied`)
  - `objective`
  - `files read`
  - `files written`
  - `skill usage`
  - `blockers/compromises`
- 산출물을 재사용했다면 원본 실행과 복사 경로를 적는다.
- `reviewer`는 단계 기록을 쓰지 않고, `REVIEW.md`와 `FEEDBACK.md` 안에 근거를 직접 인용한다.
- 같은 실행에서 동일한 `agent/worker label`이 여러 단계 산출물에 반복되면 출처 기록 실패로 보고 기본적으로 실행 절차 문제로 분류한다.

## 예상 산출물

- `cases/*/CASE.md`
- `cases/*/before/*`
- `cases/*/before/STAGE_NOTE.md`
- `cases/*/after/*`
- `cases/*/after/STAGE_NOTE.md`
- `REVIEW.md`
- `FEEDBACK.md`

## 성공 조건

- `writer`가 `structure-first` 용어를 쓰지 않고 관습적인 기준 코드를 만들었는가
- `applier`가 구조를 읽고 추적하기 어려운 구체적인 문제와 자연스러운 읽기 형태를 확인했는가
- 구조 유지, 국소 변경, 변경하지 않음을 정상 결과로 선택할 수 있었는가
- 큰 사례가 함수 수준의 과도한 분리로 무너지지 않았는가
- 복잡도를 도우미 함수 연쇄, 감싸기 계층, 문맥 객체, 설정, 숨은 상태, 오류 채널 또는 생명주기 뒤로 옮겨 숨기지 않았는가
- 모든 사례에 테스트 상태가 명시됐는가(`added`, 또는 사유·다음 안정적 책임 단위·필수 계약 사례를 포함한 `deferred`)
- 실행 근거 정보(`agent/worker id`, `fork_context`)가 단계 산출물에 보이는가
- 단계별 담당자가 실제로 분리되어 있는가(`writer`, `applier`, `reviewer`의 표지가 서로 다른가)
- 검토에서 찾은 문제가 막연한 취향 차이가 아니라 구체적인 지침 개선으로 이어지는가
