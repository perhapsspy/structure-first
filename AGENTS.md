# AGENTS.md

## 작업 원칙 (핵심)

- 외부 노출 문서만 한/영 페어를 유지한다.
  - `README`, `SKILL`, `ORIGIN`, `INSIGHTS`, examples처럼 외부에서 읽을 문서는 한/영 의미를 같이 맞춘다.
  - `SKILL.md`를 바꾸면 `SKILL.ko.md`도 의미 동기화한다.
- 내부 운영 문서는 기본적으로 한국어 단일 문서로 둔다.
  - dogfood playbook, run template, 운영 메모처럼 앞으로 저장소 운영에만 쓰는 문서는 영문 페어를 만들지 않는다.
  - 제목이나 용어에 영어가 일부 섞일 수는 있지만, 본문 설명은 한국어를 기본으로 둔다.
- 문서/스킬/템플릿 간 메시지는 하나로 맞춘다.
  - 설치 방식, 리뷰 흐름, 정책이 서로 충돌하지 않게 유지한다.
- 설치/사용 안내는 기본 흐름만 짧게 유지한다.
  - 기본 기능과 선택 기능을 명확히 분리한다.
- dogfood는 durable 자산과 disposable 산출물을 분리한다.
  - playbook과 template은 자산으로 다루고, 개별 run의 `before/after`, `REVIEW`, `FEEDBACK`는 휘발성 결과로 본다.
  - disposable dogfood output은 `docs/dogfood/runs/` 아래에만 둔다.
- 템플릿은 단일 소스로 운영한다.
  - 같은 목적의 중복 템플릿을 두지 않는다.
- `.gitignore`는 단순하게 유지한다.
  - 반복 생성되는 로컬 산출물과 disposable output만 넣고, 일회성/역사적 경로 예외를 계속 쌓아두지 않는다.
- 자동화/게시 흐름은 “기본 동작 + 실패 시 폴백” 구조로 쓴다.
- 리뷰 응답은 항상 이슈/리스크를 먼저 제시한다.
