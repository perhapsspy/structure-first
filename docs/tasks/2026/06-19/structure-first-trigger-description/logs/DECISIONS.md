**2026-06-19**

- **Background**: 최근 비자명한 코드 작업에서도 `structure-first`가 명시적으로 잘 선택되지 않는다는 문제가 있었다.
- **Decision**: global AGENTS에 새 라우팅을 추가하지 않고, `structure-first` skill frontmatter description의 trigger vocabulary를 개선한다.
- **Why**: 스킬 선택의 1차 표면은 description이며, global AGENTS는 항상-read 비용을 늘린다.
- **Impact**: 코드 shape 변경, 경계/ownership/test 계약이 걸린 작업에서 스킬 discoverability가 개선되어야 한다.
