# Goal

`structure-first-review` 스킬을 저장소에서 제거하고, 외부 노출 문서와 남은 스킬 메타데이터를 현재 배포 상태에 맞게 정리한다.

## Scope

- `skills/structure-first-review/` 한/영 스킬 문서 제거
- `README.md`, `README.en.md`에서 review 스킬 안내 제거 및 설치/사용 흐름 단순화
- 남아 있는 스킬 frontmatter의 `metadata.version` 복구
- 작업 결과 검증 후 커밋

## Current Understanding

- 현재 외부 노출 문서에서 `structure-first-review`는 `README.md`, `README.en.md`에만 직접 노출된다.
- 남아 있는 스킬 중 `skills/structure-first/SKILL.md`, `skills/structure-first-docs/SKILL.md`는 `metadata.version`이 빠진 상태다.
- `skills/structure-first-review/SKILL.md`에도 같은 변경이 있었지만 이번 작업에서는 스킬 자체를 제거한다.

## Current State

- `structure-first-review` 한/영 스킬 문서를 제거했다.
- `README.md`, `README.en.md`에서 review 스킬 설치/프롬프트 안내를 제거했다.
- `skills/structure-first/SKILL.md`, `skills/structure-first-docs/SKILL.md`에 `metadata.version: '1.0'`을 복구했다.
- `project-context` checker를 막던 과거 task의 누락 로그 파일도 최소 형태로 복원했다.

## Next Step

- 변경을 스테이징하고 하나의 커밋으로 묶는다.

## Related Docs

- `README.md`
- `README.en.md`
- `skills/structure-first/SKILL.md`
- `skills/structure-first-docs/SKILL.md`

## Working Boundary

- 이번 작업은 review 스킬 제거와 그에 직접 연결된 문서/메타데이터 정리에 한정한다.
- dogfood 문서나 내부 운영 문서의 일반적인 `review` 용어는 제거 대상이 아니다.

## Latest Validation

- 관련 참조 검색: `rg -n "structure-first-review|ai-reviews|AI Reviews" README* docs skills -S`
- 기존 워크트리 확인: `git diff -- skills/structure-first/SKILL.md skills/structure-first-docs/SKILL.md skills/structure-first-review/SKILL.md`
- `git diff --check`
- `project-context` checker 결과: `[OK] project-context current runtime shape checks`
