# Goal

`structure-first-docs`를 단일 문서 재구성 중심에서 문서 패키지 구성/리뷰까지 다루는 스킬로 확장한다.

## Scope

- `skills/structure-first-docs/SKILL.md`, `SKILL.ko.md` 의미 동기화
- Conalog `docs/tasks`의 큰 task root 사례 조사
- ChatGPT Pro 또는 별도 모델에 넘길 수 있는 조사/질문 패킷 작성

## Current Understanding

- 기존 `structure-first-docs`는 source fidelity와 단일 문서 reader flow를 잘 다루지만, 큰 `docs/tasks` 패키지의 entrypoint, routing, canonical owner, evidence/log/archive 분리까지는 명시하지 않는다.
- Conalog의 큰 task root는 코드 패키지처럼 작동한다. `README`/`BRIEF`가 진입점과 재개 상태를 맡고, root-level canonical docs가 계약/계획/gate를 소유하며, `research`, `working`, `logs`, `archive`가 증거/초안/기록/낡은 자료를 분리한다.
- 좋은 문서 패키지는 파일 수가 적은 것이 아니라 애매한 owner가 적은 상태다.

## Current State

- 대표 사례로 `edge-agent-system-design`, `edge-management-improvement`, `fieldwork` task root의 파일 구조와 진입 문서를 확인했다.
- `structure-first-docs` 한/영 스킬 문서를 package compose/review 모드까지 포함하도록 갱신했다가, 외부 GPT 피드백을 반영해 독립 스킬용 짧은 원칙 중심 버전으로 다시 줄였다.
- 특정 스킬명과 저장 구조 계약 언급은 제거했고, 기존 프로젝트 관례를 따르되 이 스킬은 의미 구조만 판단하도록 정리했다.
- 한국어판은 리뷰용 companion으로 명시하되 영문 정본과 의미를 맞춘 요약 형태로 유지한다.
- ChatGPT Pro 직접 호출 도구는 없어서, 대신 외부 모델에 그대로 넘길 수 있는 handoff 문서를 남겼다.

## Next Step

- Reopen if 실제 패키지 리뷰 dogfood에서 `Package Review` 체크리스트가 과하게 템플릿화되거나 backlog/log-heavy task를 잘못 고치려는 경향이 보이면 조정한다.

## Working Boundary

- `skills/structure-first-docs/SKILL.md`
- `skills/structure-first-docs/SKILL.ko.md`
- `docs/tasks/2026/06-02/structure-first-docs-package-skill/**`
