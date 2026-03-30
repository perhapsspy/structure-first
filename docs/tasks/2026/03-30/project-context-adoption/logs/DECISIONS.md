**2026-03-30**

- 결정: 이 저장소는 최신 `project-context` 런타임 shape인 `docs/reference/`와 `docs/tasks/...`를 바로 도입한다.
- 이유: README 문구만으로는 새 규칙이 실제 작업 루프에 반영되지 않고, dogfood template도 portable path 규칙과 충돌하고 있었다.
- 대안: README 설명만 수정하는 방안은 검토했지만, 저장소 내부 운영 흐름과 checker 검증 대상이 비어 남아 규칙 적용이 불완전해서 채택하지 않았다.
- 영향: 이후 write-bearing 작업은 기본적으로 날짜별 task를 남기고, 재사용 규칙은 reference 문서로 관리하며, dogfood run 산출물은 disposable로 유지한다.
