# Goal

`structure-first` 스킬이 비자명한 코드 생성/수정/리팩터링/리뷰 작업에서 더 잘 선택되도록 frontmatter description을 다듬고 로컬 설치본까지 갱신한다.

## Scope

- `skills/structure-first/SKILL.md` description trigger wording 개선
- `skills/structure-first/SKILL.ko.md` 의미 동기화
- repo 배포와 global 로컬 설치본 업데이트

## Current Understanding

- 스킬 선택의 1차 표면은 `SKILL.md` frontmatter의 `name`과 `description`이다.
- 현재 description은 구조 철학 요약은 되지만, 실제 trigger vocabulary가 약하다.
- 새 wording은 자기지시형 표현 없이 비자명한 코드 shape 변경, 경계, orchestration, ownership, side effect, async/state, test 계약 표면을 잡아야 한다.

## Current State

- `deep_reasoner` 검토를 반영해 자기지시형 표현 없이 trigger vocabulary 중심으로 한/영 문구를 수정했다.
- `git diff --check`, `quick_validate.py`, `project-context` shape check가 통과했다.
- 로컬 global 설치본은 `structure-first`로 설치되어 있다.

## Next Step

- commit/push와 local update를 완료한다.

## Working Boundary

- `skills/structure-first/SKILL.md`
- `skills/structure-first/SKILL.ko.md`
- `docs/tasks/2026/06-19/structure-first-trigger-description/`
