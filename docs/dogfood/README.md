# Dogfood Playbook

## Purpose

이 폴더는 도그푸딩 절차와 템플릿을 정리하는 내부 운영 문서다.
개별 run은 `docs/dogfood/runs/` 아래에서 만들고 필요할 때만 남긴다.

## Recommended Run Layout

새 run은 아래 형태를 기본으로 한다.

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

## Standard Loop

1. 목표를 한 줄로 고정한다.
2. 새 run 디렉터리를 만들고 template 파일을 복사한다.
3. `CASE.md`에 scale, writer brief, applier goal, reviewer focus를 적는다.
4. writer stage를 돌린다.
   writer는 skill을 읽지 않고 `before`와 `before/STAGE_NOTE.md`만 만든다.
5. applier stage를 돌린다.
   applier는 matching `before`와 target skill만 읽고 `after`와 `after/STAGE_NOTE.md`만 만든다.
6. reviewer stage를 돌린다.
   reviewer는 `before/after`, stage note, current skill, 그리고 회귀 비교가 필요할 때만 이전 feedback을 읽고 `REVIEW.md`, `FEEDBACK.md`를 만든다.
7. 컴파일/포맷/기본 검증을 돌린다.
8. 결론을 분류한다.
   skill 문제면 `SKILL.md`와 pair 문서를 수정한다.
   pipeline 문제면 template와 playbook을 수정한다.
   example artifact 문제면 run output만 고친다.
9. 통찰이 반영되면 run output은 보관 또는 삭제한다.

## Context Hygiene Rules

- stage마다 case당 한 에이전트만 쓴다.
- `fork_context=false`를 기본으로 해서 대화 문맥 오염을 막는다.
- write scope는 case와 stage 단위로 분리한다.
- writer/applier는 항상 `STAGE_NOTE.md`를 남긴다.
- stage note에는 최소한 아래 항목을 남긴다.
  - `run root`
  - `agent/worker id`
  - `fork_context`
  - `artifact status`
  - `objective`
  - `files read`
  - `files written`
  - `skill usage`
  - `blockers/compromises`
- artifact를 재사용했다면 source run과 copied path를 note에 적는다.
- reviewer는 stage note를 쓰지 않고, `REVIEW.md`와 `FEEDBACK.md` 안에서 파일 근거를 직접 인용한다.

## Default Scope

- 기본 코드는 `readability/scale-guidance dogfood`로 본다.
- test file이 case brief에 없으면 applier는 테스트를 추가하지 않고 `deferred`와 다음 stable Atom, required contract cases를 남긴다.
- full testing pillar 검증이 목적일 때만 test file을 case set에 포함한다.

## Change Triage

도그푸딩 뒤 무엇을 바꿀지는 아래 기준으로 나눈다.

- 같은 문제가 여러 case나 여러 scale에서 반복되면 `skill` 수정
- provenance, read boundary, run scope가 애매하면 `pipeline/template` 수정
- 한 example만 잘못 생성됐고 skill 문구와는 충돌하지 않으면 `run artifact` 수정

즉, run 결과에서 바로 skill을 고치기보다 먼저 `문제의 owner`를 분리한다.

## Success Checks

- writer가 skill vocabulary 없이 plausible baseline을 만들었는가
- applier가 current unit을 유지한 채 readable primary flow를 만들었는가
- reviewer가 issues/risks first로 판단했는가
- provenance, execution proof, stage separation이 artifact만으로 읽히는가
- 결과가 skill 변경인지, pipeline 변경인지, example 수정인지 분류됐는가

## Next Run

다음 code dogfood는 아래 순서로 시작하면 된다.

1. `docs/dogfood/runs/<new-run-name>/` 생성
2. [templates/structure-first-scale/PIPELINE.md](templates/structure-first-scale/PIPELINE.md) 복사
3. case 수만큼 [templates/structure-first-scale/CASE.md](templates/structure-first-scale/CASE.md) 복사
4. writer/applier는 [templates/structure-first-scale/STAGE_NOTE.md](templates/structure-first-scale/STAGE_NOTE.md) 형식에 맞춰 각 case의 stage note를 남긴다
5. reviewer는 [templates/structure-first-scale/REVIEW.md](templates/structure-first-scale/REVIEW.md), [templates/structure-first-scale/FEEDBACK.md](templates/structure-first-scale/FEEDBACK.md) 구조를 기준으로 작성한다
6. review 결과를 `skill / pipeline / artifact`로 분류
