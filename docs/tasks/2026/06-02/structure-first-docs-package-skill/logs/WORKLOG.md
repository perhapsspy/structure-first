# Worklog

**2026-06-02**

- 기존 `structure-first-docs`와 `project-context` 스킬 본문을 읽고, 둘 사이의 책임 경계를 확인했다.
- Conalog `docs/tasks`에서 파일 수가 많은 task root를 검색하고 `edge-agent-system-design`, `edge-management-improvement`, `fieldwork`를 대표 사례로 골랐다.
- 대표 사례의 `README`, `BRIEF`, root-level canonical docs, `research`, `working`, `archive`, `logs` 배치를 확인해 문서 패키지 품질 기준을 도출했다.
- ChatGPT Pro 직접 연결 도구는 없음을 확인하고, 대신 외부 모델에 넘길 수 있는 조사 패킷을 task-local working 자료로 남기는 방향으로 정했다.
- 독립 `deep_planner` 검토 결과를 반영해 backlog style, migration/demotion, reference candidate, append-only log sampling, parent-owned decision 기준을 스킬에 추가했다.
- 조사 패킷의 `Observed Examples`가 경로 목록에 가까워 GPT Pro에 바로 넘기기 부족하다는 피드백을 반영해, 각 사례의 구조/소유권/위험을 본문 설명으로 풀어 썼다.
- 외부 GPT 피드백을 반영해 스킬 본문을 독립 스킬용 짧은 원칙 중심 구조로 다시 썼다. 특정 스킬명과 경로 계약은 제거했고, 반복되던 `Core Rules`/`Execution Steps`/`Final Checks`는 `Principles`, `Package Roles`, `Compose Rules`, `Review Rules`, `Output Contract`로 압축했다.
- 2차 GPT 피드백을 반영해 `parent-owned`, `root-level`, `task roots`처럼 독립 스킬에서 애매한 표현을 일반화하고, owner 선택은 source 또는 기존 관례가 명확할 때만 하도록 제한했다.
- 웹에서 확인한 skill authoring 기준을 반영해 frontmatter `description`을 더 구체적인 trigger vocabulary 중심으로 확장했다. `design docs`, `implementation plans`, `migration plans`, `runbooks`, `handoffs`, `task-doc bundles`, `documentation sets` 같은 실제 사용자 요청 표현을 포함했다.
