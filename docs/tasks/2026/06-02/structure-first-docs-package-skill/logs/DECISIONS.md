# Decisions

**2026-06-02**

- **Background**: 기존 `structure-first-docs`는 단일 문서 재구성/리뷰 중심이라 큰 task root의 문서 패키지 품질을 다루는 어휘가 부족했고, 1차 확장안은 특정 스킬명/경로 계약/반복 체크리스트가 많아 독립 스킬과 토큰 효율에 맞지 않았다.
- **Decision**: 최종 스킬 본문은 `Document Compose/Review`와 `Package Compose/Review`를 유지하되, 특정 스킬명을 빼고 저장 구조는 기존 프로젝트 관례에 맡기며 원칙/역할/출력 계약 중심의 짧은 버전으로 줄인다.
- **Why**: 큰 설계/운영 작업의 품질 문제는 entrypoint, owner, gate/runbook, evidence/log/archive 분리에서 발생하지만, 장기적으로는 세부 절차보다 좋은 결과의 불변 조건과 리뷰 출력 계약이 더 유지보수하기 쉽다.
- **Impact**: `SKILL.md`는 독립 스킬로 일반화되고, `SKILL.ko.md`는 리뷰용 companion으로 격하하되 의미 요약은 유지한다.
