**2026-03-31**

- 결정: 상태 owner와 async contract 보강 방향은 유지하되, core skill 본문에서는 프런트엔드 고유 어휘와 과한 새 추상화는 줄이는 방향으로 축소 수정한다.
- 이유: 리뷰와 서브에이전트 의견이 공통으로 “넣을 내용은 맞지만, core skill 치고는 too specific”하다고 지적했다.
- 대안: 기존 문구를 유지하고 examples에서만 보완하는 방안도 있었지만, 본문 자체가 review finding을 받고 있어 wording을 바로 정리하는 쪽을 택했다.
- 영향: 구조 원칙은 유지하면서도 `structure-first`의 범용 포지션과 문서 일관성이 더 좋아진다.
- 결정: `single-writer` 계열 문장은 절대 규칙보다 기본 bias로 읽히게 낮추고, multi-writer coordination이 책임인 경우 explicit coordinator를 허용한다.
- 이유: 최근 리뷰에서 legitimate coordinated-writer 구조와 benign local adaptation까지 과하게 누를 수 있다는 residual risk가 반복됐다.
