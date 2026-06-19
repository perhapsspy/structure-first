# Goal

`structure-first` 스킬이 지엽적/기계적 수정이 아닌 대부분의 코드 작업에서 더 자연스럽게 선택되도록 frontmatter description을 다듬고 로컬 설치본까지 갱신한다.

## Scope

- `skills/structure-first/SKILL.md` description trigger wording 개선
- `skills/structure-first/SKILL.ko.md` 의미 동기화
- repo 배포와 global 로컬 설치본 업데이트

## Current Understanding

- 스킬 선택의 1차 표면은 `SKILL.md` frontmatter의 `name`과 `description`이다.
- 현재 description은 구조 철학 요약은 되지만, 실제 trigger vocabulary가 약하다.
- 새 wording은 자기지시형 표현 없이 코드 생성, 기능 작업, 버그 수정, 리팩터링, 리뷰 전반에서 Primary Flow, 최소 경계, decision ownership, side-effect isolation, async/state clarity, test 계약 표면을 잡아야 한다.

## Current State

- `deep_reasoner` 재검토를 반영해 "비자명한 코드" 표현을 제거하고, 작은데 위험한 버그 수정을 배제하지 않도록 `Skip only` 기준으로 한/영 문구를 수정했다.
- `git diff --check`, `quick_validate.py`, `project-context` shape check가 통과했다.
- repo `main`에 commit `7dbb6f1`을 push했다.
- `npx skills update structure-first -g -y`로 global 로컬 설치본을 갱신했고, 설치본의 한/영 문구가 repo와 일치한다.

## Next Step

- Reopen if recent coding tasks still fail to trigger `structure-first` after this description update.

## Working Boundary

- `skills/structure-first/SKILL.md`
- `skills/structure-first/SKILL.ko.md`
- `docs/tasks/2026/06-19/structure-first-trigger-description/`
