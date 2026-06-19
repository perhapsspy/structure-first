**2026-06-19**

- 사용자 요청에 따라 global AGENTS 라우팅이 아니라 `structure-first` 스킬 자체의 description trigger wording을 개선하는 방향으로 범위를 고정했다.
- `project-context`와 `skill-creator` 기준을 다시 확인했고, 스킬 선택에는 frontmatter description이 핵심이라는 점을 반영했다.
- repo 상태, 기존 README 설치 안내, global 설치 상태를 확인했다.
- 최종 문구는 자기지시형 표현을 피하도록 `deep_reasoner`에 별도 검토를 요청했다.
- `deep_reasoner`의 trigger vocabulary 제안을 반영해 `SKILL.md` description을 `Non-trivial code generation/editing/refactoring/review` 표면과 flow/boundary/ownership/test 계약 중심으로 수정했다.
- `SKILL.ko.md`에는 같은 의미를 한국어 설명 동기화 문장으로 추가했다.
- `git diff --check`, 임시 `PyYAML` target을 사용한 `quick_validate.py skills/structure-first`, `project-context` shape check를 실행해 통과를 확인했다.
- `structure-first 스킬 description 트리거 개선` commit을 `main`에 push한 뒤 `npx skills update structure-first -g -y`로 global 설치본을 갱신했다.
- global 설치본의 `structure-first/SKILL.md`와 `SKILL.ko.md`를 확인해 description과 한국어 동기화 문장이 repo와 일치함을 확인했다.
