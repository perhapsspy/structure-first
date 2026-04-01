**2026-03-31**

- 현재 `SKILL.md` / `SKILL.ko.md` 변경분과 전 턴 리뷰 findings를 다시 읽었다.
- 서브에이전트 리뷰 내용을 브레인스토밍 입력으로 재사용해 anti-pattern 문장 일반화, async contract/strategy 분리, 새 gate 부담 축소 쪽으로 방향을 좁혔다.
- 오늘 날짜 task를 만들고, core skill 본문만 축소 수정하기로 범위를 고정했다.
- `SKILL.md`와 `SKILL.ko.md`에서 frontend-specific 표현을 일반화하고, async 문장을 freshness/completion contract 중심으로 다듬었다.
- `Meaning state` 별도 정의는 제거하고 `Completion Evidence`의 `Tests` 줄에 관련 contract를 적을 수 있게 조정했다.
- `git diff --check`와 `project-context` checker를 실행해 현재 워킹트리 기준 문법/런타임 shape 이상이 없음을 확인했다.
- 후속 리뷰를 반영해 async 문장의 `latest-wins` 뉘앙스를 제거하고, `externally meaningful ...` 표현은 `externally observed state` 수준으로 더 낮췄다.
- 후속 서브에이전트 리뷰에서 남은 residual risk를 반영해 `single-writer` 규칙을 default bias로 낮추고, `mirror-sync`와 `self-feedback` 문장을 더 직접적인 비교 단위로 정리했다.

**2026-04-01**

- 후속 리뷰에서 남은 `observable outcome` vs `externally observable result` 용어 불일치를 확인했다.
- `SKILL.md`와 `SKILL.ko.md`의 ownership 문구를 기존 `Equivalent path` 언어에 맞춰 한 축으로 정렬했다.
- `BRIEF.md` current state와 next step도 최신 wording loop 상태에 맞게 다시 썼다.
