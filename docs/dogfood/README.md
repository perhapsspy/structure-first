# Dogfood Playbook

## 목적

이 폴더는 도그푸딩 절차와 템플릿을 정리하는 내부 운영 문서다.
개별 실행은 `docs/dogfood/runs/` 아래에서 만들고 필요할 때만 남긴다.

## 권장 실행 구조

새 실행은 아래 형태를 기본으로 한다.

```text
docs/dogfood/runs/<run-name>/
  PIPELINE.md
  REVIEW.md
  FEEDBACK.md
  cases/
    <case-name>/
      CASE.md
      before/
        STAGE_NOTE.md
      after/
        STAGE_NOTE.md
```

`<run-name>`은 `skill-topic-vN` 또는 `skill-topic-YYYYMMDD`처럼 목적이 보이게 짓는다.

## 표준 절차

1. 목표를 한 줄로 고정한다.
2. 새 실행 디렉터리를 만들고 틀 파일을 복사한다.
3. `CASE.md`에 사례 규모, `writer` 작업 설명, `applier` 목표와 `reviewer` 검토 관점을 적는다.
4. `writer` 단계를 돌린다.
   `writer`는 스킬을 읽지 않고 `before`와 `before/STAGE_NOTE.md`만 만든다.
   각 사례의 `writer`는 전담 하위 에이전트 하나가 맡고, 같은 `agent/worker label`을 다른 단계에 재사용하지 않는다.
5. `applier` 단계를 돌린다.
   `applier`는 해당 `before`와 대상 스킬만 읽고 `after`와 `after/STAGE_NOTE.md`만 만든다.
   각 사례의 `applier`는 해당 `writer`와 다른 전담 하위 에이전트가 맡는다.
6. `reviewer` 단계를 돌린다.
   `reviewer`는 `before/after`, 단계 기록, 현재 스킬, 그리고 회귀 비교가 필요할 때만 이전 개선 의견을 읽고 `REVIEW.md`, `FEEDBACK.md`를 만든다.
   `reviewer`는 어떤 `writer`나 `applier`와도 다른 하위 에이전트여야 한다.
7. 컴파일/포맷/기본 검증을 돌린다.
8. 결론을 분류한다.
   스킬 문제면 `SKILL.md`와 짝 문서를 수정한다.
   실행 절차 문제면 틀과 운영 지침을 수정한다.
   예시 산출물 문제면 실행 결과만 고친다.
9. 통찰이 반영되면 실행 결과는 보관하거나 삭제한다.

## 문맥 분리 규칙

- 단계마다 사례당 한 에이전트만 쓴다.
- `fork_context=false`를 기본으로 해서 대화 문맥 오염을 막는다.
- 같은 사례에서 `writer`와 `applier`에 같은 `agent/worker label`을 쓰지 않는다.
- `reviewer`는 `writer`·`applier`와 다른 `agent/worker label`이어야 한다.
- 메인 에이전트는 실행 틀과 단계 조정까지만 맡고, `before/after/REVIEW/FEEDBACK` 산출물 작성자는 하위 에이전트로 분리하는 것을 기본으로 한다.
- 쓰기 범위는 사례와 단계 단위로 분리한다.
- `writer`와 `applier`는 항상 `STAGE_NOTE.md`를 남긴다.
- 단계 기록에는 최소한 아래 항목을 남긴다.
  - `run root`
  - `agent/worker id`
  - `fork_context`
  - `artifact status`
  - `objective`
  - `files read`
  - `files written`
  - `skill usage`
  - `blockers/compromises`
- 산출물을 재사용했다면 원본 실행과 복사 경로를 기록에 적는다.
- `reviewer`는 단계 기록을 쓰지 않고, `REVIEW.md`와 `FEEDBACK.md` 안에서 파일 근거를 직접 인용한다.
- 같은 실행에서 동일한 `agent/worker label`이 여러 단계 산출물에 반복되면 출처 기록 실패로 보고 기본적으로 실행 절차 문제로 분류한다.

## 기본 범위

- 기본 코드는 읽기 쉬움과 규모별 지침을 검증하는 대상으로 본다.
- 테스트 파일이 사례 설명에 없으면 `applier`는 테스트를 추가하지 않고 `deferred` 사유, 다음으로 테스트할 안정적인 책임 단위와 필요한 계약 사례를 남긴다.
- 테스트 지침 전체를 검증하는 것이 목적일 때만 테스트 파일을 사례 묶음에 포함한다.

## 변경 분류

도그푸딩 뒤 무엇을 바꿀지는 아래 기준으로 나눈다.

- 같은 문제가 여러 사례나 여러 규모에서 반복되면 `skill` 수정
- 출처 기록, 읽기 경계, 실행 범위가 애매하면 `pipeline/template` 수정
- 한 예시만 잘못 생성됐고 스킬 문구와는 충돌하지 않으면 실행 산출물 수정

즉, 실행 결과만 보고 바로 스킬을 고치기보다 먼저 문제를 어디에서 고쳐야 하는지 구분한다.

## 성공 조건

- `writer`가 `structure-first` 용어를 쓰지 않고 관습적인 기준 코드를 만들었는가
- `applier`가 구조를 읽고 추적하기 어려운 구체적인 문제와 자연스러운 읽기 형태를 확인했는가
- 구조 유지, 국소 변경, 변경하지 않음을 정상 결과로 선택할 수 있었는가
- 복잡도를 도우미 함수 연쇄, 감싸기 계층, 문맥 객체와 생명주기 뒤로 옮겨 숨기지 않았는가
- `reviewer`가 문제와 위험을 먼저 판단했는가
- 출처 기록, 실행 근거와 단계 분리가 산출물만으로 읽히는가
- 결과가 스킬, 실행 절차, 예시 중 어디를 고칠 문제인지 분류됐는가

## 다음 실행

다음 코드 도그푸딩은 아래 순서로 시작하면 된다.

1. `docs/dogfood/runs/<new-run-name>/` 생성
2. [templates/structure-first-scale/PIPELINE.md](templates/structure-first-scale/PIPELINE.md) 복사
3. 사례 수만큼 [templates/structure-first-scale/CASE.md](templates/structure-first-scale/CASE.md) 복사
4. `writer`와 `applier`는 [templates/structure-first-scale/STAGE_NOTE.md](templates/structure-first-scale/STAGE_NOTE.md) 형식에 맞춰 각 사례의 단계 기록을 남긴다
5. `reviewer`는 [templates/structure-first-scale/REVIEW.md](templates/structure-first-scale/REVIEW.md), [templates/structure-first-scale/FEEDBACK.md](templates/structure-first-scale/FEEDBACK.md) 구조를 기준으로 작성한다
6. 검토 결과를 스킬, 실행 절차, 산출물 문제로 분류
