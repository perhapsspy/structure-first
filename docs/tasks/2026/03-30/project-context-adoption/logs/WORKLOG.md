**2026-03-30**

- 저장소 전역 검색으로 `project-context`, `docs/tasks`, `docs/reference`, `BRIEF.md`, `DECISIONS.md`, `WORKLOG.md` 관련 흔적을 확인했다.
- 현재 저장소에는 `docs/reference/`와 `docs/tasks/...`가 없고, `project-context` 직접 언급은 README 한/영 문구에만 있다는 점을 확인했다.
- dogfood `STAGE_NOTE.md` 템플릿이 절대 경로를 요구하는 것을 확인했고, 이를 portable path 규칙 위반으로 분류했다.
- `docs/reference/project-context.md`와 이번 변경용 task 문서를 추가하고, README 및 dogfood playbook/template를 새 규칙에 맞게 수정했다.
- portable path 문자열을 다시 점검한 뒤 `project-context` checker를 저장소 루트 기준으로 실행했고 `[OK] project-context current runtime shape checks`를 확인했다.
