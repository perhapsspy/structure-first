# Goal

`structure-first`의 smallest-current-unit 장점을 유지하면서, 변경 뒤 실제 ownership closure가 깨졌다는 증거가 있을 때만 가장 작은 미해결 단위로 다시 진입하게 한다.

## Scope

- `skills/structure-first/SKILL.md`와 `SKILL.ko.md`의 stay-local·boundary witness·unresolved 처리만 최소 수정하고 독립 forward-test로 검증한다.
- core skill에 recursive loop, Goal/Codex 결합, 파일 수·크기 trigger, 장황한 witness 예시를 넣지 않는다.
- 검증된 한·영 source와 task context를 canonical `main`에 publish하고 Project Legibility 0.7.1 patch handoff용 commit을 확정한다. Release, tag, downstream sync는 이 작업에서 수행하지 않는다.

## Current Understanding

- focused verification으로 작업을 current unit에 두되, 다른 owner의 evidence가 나오면 가장 작은 implicated unit만 다시 연다.
- identity, authoritative data, external write, runtime·async boundary의 중요한 claim은 boundary owner의 nearest safe witness로 검증한다.
- safe witness가 없으면 boundary와 다음 check·responsible unit·cases를 unresolved로 남기며 local tests만으로 닫지 않는다.

## Current State

- 독립 forward-test와 최종 리뷰가 무결함으로 닫혔고 사용자가 canonical publish를 승인했다.
- evidence-gated ownership closure는 영문 46줄·국문 44줄을 유지하며 trigger나 제품 역할을 바꾸지 않는 core-contract patch로 확정됐다.
- frontmatter, `agents/openai.yaml`, README, dogfood, examples는 변경하지 않았다.

## Next Step

- Canonical `main` commit SHA를 Project Legibility 0.7.1 patch handoff의 source로 전달한다.

## Working Boundary

- `skills/structure-first/SKILL.md`
- `skills/structure-first/SKILL.ko.md`
- `docs/tasks/2026/08-03/evidence-gated-ownership-closure/`
