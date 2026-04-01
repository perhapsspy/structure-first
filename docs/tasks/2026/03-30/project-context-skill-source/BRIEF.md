# Goal

이 저장소의 작업 맥락 운영 기준을 repo-local reference 문서가 아니라 `project-context` 스킬과 `AGENTS.md`에 두도록 정리한다.

## Scope

- `AGENTS.md`에 `project-context` 사용 원칙 명시
- 중복 설명이 된 `docs/reference/project-context.md` 삭제
- 이번 정리 작업을 날짜별 task로 기록
- 변경 후 `project-context` checker 재검증

## Current Understanding

- 이 저장소는 이미 `docs/reference/`와 `docs/tasks/...` 런타임 shape를 사용 중이다.
- `docs/reference/project-context.md`는 스킬이 없을 때 저장소 안에 임시로 두었던 운영 규칙 문서 역할을 했다.
- 이제는 스킬 본문이 canonical source이므로, 저장소에는 프로젝트 고유 rule만 남기고 스킬 계약 복제는 제거하는 편이 더 일관된다.

## Current State

- `AGENTS.md`에 `project-context` 사용 원칙과 중복 문서 금지 규칙을 추가했다.
- repo-local duplicate였던 `docs/reference/project-context.md`를 삭제했다.
- 이번 변경을 위한 task 문서를 추가했다.

## Next Step

- 이후 `project-context` 관련 저장소 규칙이 생기면 스킬 본문 복제가 아니라 이 저장소 고유 차이점만 `docs/reference/` 또는 `AGENTS.md`에 남긴다.
- 후속 문서 변경에서도 task/reference 경계가 유지되는지 본다.

## Related Docs

- `AGENTS.md`
- `docs/tasks/2026/03-30/project-context-adoption/BRIEF.md`
- `$CODEX_HOME/skills/project-context/SKILL.md`

## Working Boundary

- 이번 작업은 저장소 운영 문서 정렬에 한정한다.
- public README/skill 본문은 건드리지 않는다.

## Latest Validation

- 변경 후 `project-context` checker를 저장소 루트에서 다시 실행해 runtime shape를 확인한다.
