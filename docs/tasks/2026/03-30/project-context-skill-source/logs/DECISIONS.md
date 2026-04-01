**2026-03-30**

- 결정: 저장소 안의 `project-context` 운영 기준은 repo-local reference 문서보다 설치된 `project-context` 스킬과 `AGENTS.md`를 source of truth로 둔다.
- 이유: `docs/reference/project-context.md`는 스킬 계약을 거의 그대로 복제하는 상태여서, 둘이 어긋날수록 운영 기준이 둘로 갈라질 위험이 있다.
- 대안: reference 문서를 유지하면서 스킬과 수동 동기화하는 방안도 가능하지만, 이 저장소 고유 규칙과 스킬 계약의 경계가 다시 흐려져 채택하지 않았다.
- 영향: 이후 저장소에는 프로젝트 고유 운영 규칙만 남기고, `project-context` 공통 계약은 스킬 본문과 `AGENTS.md` 언급을 기준으로 해석한다.
