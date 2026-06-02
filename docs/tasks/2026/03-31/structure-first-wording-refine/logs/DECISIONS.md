**2026-03-31**

- **Background**: 리뷰와 서브에이전트 의견이 상태 owner와 async contract 보강 방향은 맞지만 core skill 본문 치고는 프런트엔드 고유 어휘와 새 추상화가 과하다고 지적했다.
- **Decision**: 상태 owner와 async contract 보강 방향은 유지하되 wording을 축소하고, `single-writer` 계열 문장은 절대 규칙보다 기본 bias로 낮춰 explicit coordinator가 책임인 multi-writer coordination을 허용한다.
- **Why**: 본문 자체가 review finding을 받고 있었고, 최근 리뷰에서 legitimate coordinated-writer 구조와 benign local adaptation까지 과하게 누를 수 있다는 residual risk가 반복됐기 때문이다.
- **Impact**: 구조 원칙은 유지하면서도 `structure-first`의 범용 포지션과 문서 일관성이 더 좋아진다.
