# Goal

`structure-first-docs`가 사용자 정정, 삭제 지시, 간결성 요구를 새 설명으로 증식하지 않고 기존 소유 문서를 먼저 고치도록 스킬 문구를 개선한다.

## Scope

- `skills/structure-first-docs/SKILL.md` 개선
- `skills/structure-first-docs/SKILL.ko.md` 의미 동기화
- playground 조사 결과 중 실제 스킬 개선에 필요한 내용만 사용

## Current Understanding

- 반복 실패의 핵심은 문서가 부족한 것이 아니라, 현재 결론을 맡은 문서를 고치지 않고 새 설명, 안내 문서, 예외, 방어문을 덧붙이는 데 있다.
- 특히 세 패턴이 중요하다: 근거 없는 레거시 독자 상상, 최신 지적의 방어문 증식, 삭제할 내용을 금지문으로 보존.
- `structure-first-docs`는 이미 소유 문서, 중복, 격하를 다루므로 새 스킬이나 `AGENTS.md` 보강보다 기존 `Compose Rules`에 짧은 보강을 넣는 방향이 맞다.
- 이 리포는 `SKILL.md`를 바꾸면 `SKILL.ko.md`도 의미를 맞춰야 한다.

## Current State

- `skills/structure-first-docs/SKILL.md`의 `Compose Rules`에 기존 소유 문서 우선 수정, 사용자 정정/삭제 지시의 편집 입력 처리, 제거 대상의 방어문·중복 경로 보존 금지를 반영했다.
- `structure-first-docs` description은 `engineering docs`보다 넓은 `project docs`로 조정했고, `clean up`, `audit`, `source-of-truth ownership`, `current-vs-stale cleanup`, `task docs`, `handoffs`를 앞쪽 trigger로 올렸다.
- `skills/structure-first-docs/SKILL.ko.md`도 같은 의미로 동기화했다.
- frontmatter 필드 검사, `git diff --check`, `project-context` runtime shape 검사가 통과했다.

## Next Step

리포 변경은 완료됐다. 커밋/푸시와 로컬 설치본 갱신 후 닫는다.

## Working Boundary

- `skills/structure-first-docs/SKILL.md`
- `skills/structure-first-docs/SKILL.ko.md`
- `docs/tasks/2026/06-23/structure-first-docs-correction-editing/`
