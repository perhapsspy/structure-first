**2026-03-30**

- 결정: `structure-first`는 기존 `decision owner` 개념을 유지하되, 같은 의미 상태의 write owner와 async freshness/completion contract까지 명시하는 방향으로 보강한다.
- 이유: backoffice 사례의 반복 실패는 프레임워크 문법 문제가 아니라 ownership과 boundary contract의 빈틈에 더 가까웠고, 이는 core skill 철학 안에서 일반화 가능하다.
- 대안: Svelte 전용 반응성 규칙이나 렌더러/성능 전술을 본문에 직접 넣는 방안도 검토했지만, core skill이 프런트엔드 편향으로 보일 위험이 있어 채택하지 않았다.
- 영향: 이후 `structure-first`는 상태/비동기 구조 문제를 다룰 때도 더 직접적인 ownership language를 제공하게 된다.

