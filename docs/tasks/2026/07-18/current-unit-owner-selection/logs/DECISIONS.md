# Decisions

**2026-07-18**

- **Background:** current unit을 증상이 보이는 위치에서 바로 고르면 실제 규칙 owner보다 짧거나 좁은 단위에 예외 상태와 분기가 쌓일 수 있지만, frontend lifecycle 표현을 core skill에 넣으면 범용성이 훼손된다.
- **Decision:** Operating Model 첫 문장을 바꾸려는 behavior 또는 rule을 책임지는 가장 작은 current unit을 고르고 증상이나 결과의 위치만 따르지 않도록 교체한다.
- **Why:** 책임 기준은 pure function, backend, systems, batch, concurrent와 CLI 코드에 공통으로 적용되고, `smallest`는 change boundary나 verification scope를 current unit으로 부풀리는 것을 막는다.
- **Impact:** current-unit 선택 기준만 선명해지며 trigger, skill 역할, 공개 metadata와 인접 스킬 경계는 바뀌지 않는다.
