**2026-04-01**

- 기존 `structure-first-wording-20260401` run의 약점이 provenance 부족이라는 사용자 지적을 확인했다.
- dogfood playbook, pipeline template, stage note template를 읽고 distinct subagent 규칙과 provenance failure 분류 규칙을 추가했다.
- rerun용 날짜별 task를 만들고, 메인 에이전트는 scaffold/orchestration까지만 맡기로 범위를 고정했다.
- rerun용 `structure-first-wording-rerun-20260401` run을 만들고 `PIPELINE`, `CASE`, 빈 `REVIEW/FEEDBACK`를 준비했다.
- writer 3명을 `fork_context=false`로 분리 실행해 각 case의 `before` artifact와 `before/STAGE_NOTE.md`를 생성했다.
- applier 3명을 writer와 다른 subagent로 분리 실행해 각 case의 `after` artifact와 `after/STAGE_NOTE.md`를 생성했다.
- reviewer 1명을 별도 subagent로 실행해 rerun `REVIEW.md`, `FEEDBACK.md`를 작성했고 provenance 개선과 남은 `pipeline / artifact` owner를 정리했다.
- `git diff --check`와 `project-context` checker를 실행해 현재 워킹트리 기준 문법/런타임 shape 이상이 없음을 확인했다.
