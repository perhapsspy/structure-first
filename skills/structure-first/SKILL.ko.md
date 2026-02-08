# Skill: Structure First (Korean Pair)

> 영문 기본 문서: `SKILL.md`

## Purpose

> **Primary Flow**: 로직을 위에서 아래로 읽히게 만드는 메인 성공 경로

코드 생성, 리팩터링, 리뷰 시 **읽히는 성공 흐름(Primary Flow)**을 최우선으로 둡니다.  
경계는 필요한 만큼만 두고, **역할이 고정된 Atom**으로 조합합니다.  
테스트는 구현 추종이 아니라 **계약 중심(contract-driven)**으로 안정성을 확보합니다.

## When to Use

- 코드가 위에서 아래로 자연스럽게 읽히지 않을 때
- 함수/모듈 분해가 과도해지고 유틸이 늘어날 때
- 테스트가 구현 세부를 따라가며 쉽게 깨질 때

## Do Not Use

- 1회성 실험/탐색 코드
- 아주 작은 수정인데 구조 개입이 과해지는 경우

## Priorities (Bias)

- 읽히는 흐름 > 구조적 단순성 > 재사용성 > 추상화
- 미래 가능성보다 **현재 코드의 명확성** 우선
- 분해는 목적이 아니라, 읽힘이 좋아질 때만 수행

## Work Routine

1. **Intent 고정**
- 변경/코드가 하는 일을 한 문장으로 명시

2. **Boundary 최소화**
- 단계를 I/O, 도메인 판단, 변환으로 구분
- 경계는 필요한 만큼만 유지

3. **Primary Flow 먼저**
- 성공 흐름이 위→아래로 한 번에 읽히게 구성
- 분기/예외는 메인 흐름을 끊지 않게 처리(early return 등)

4. **Atom 도출**
- Primary Flow 문장이 함수로 분리될 때 더 읽히면 분리
- Atom은 역할 고정 + I/O 명확
- 가능하면 순수 함수 선호

5. **Composition 한 곳**
- 오케스트레이션은 한 위치에서만 수행
- Atom 간 직접 의존/호출 최소화

6. **Side Effects를 Boundary로**
- I/O, 상태 변경 같은 부작용은 경계에 모음
- 내부 로직은 계산/판단 중심으로 유지

7. **Read Order 정렬**
- export/public -> orchestrator -> atoms -> utils 순으로 배치

## Test Guidance (Unit tests for Atoms)

- 가능한 한 Atom 단위 유닛 테스트를 충분히 작성
- 구현 세부가 아니라 **계약(I/O, 불변조건, 경계값)**을 검증
- 테스트 코드도 읽히게 유지:
  - `each`/table 케이스로 중복 축소
  - 작은 헬퍼/팩토리는 허용하되 구조를 흐리면 중단
  - 테스트 하나는 핵심 주장 하나를 드러내기

## Stop Rules / Anti-patterns

- 분리 후 인자/상태 전달이 늘어나면 되돌리기
- 보기 좋으려고만 함수/파일 분리하지 않기(유틸 난립 금지)
- 이름이 설명문처럼 길어지면 경계를 재검토
- 미래 재사용 가정의 추상화/레이어 추가 지양
- 테스트에서 과도한 추상화/헬퍼 난립 지양

## Output Expectations

- Intent: 1줄
- Primary Flow: top-down 흐름
- Boundaries: I/O / domain / transform
- Atoms: name + I/O
- Tests: contract + edge cases + table cases
- Changes: 읽히는 흐름 개선에 집중한 타깃 변경

## Final Gates

- 성공 흐름이 위→아래로 한 번에 보이는가?
- 분리가 실제 책임/경계 변화에 대응하는가?
- Atom I/O를 한 줄로 설명 가능한가?
- 부작용이 경계에 모여 있는가?
- 테스트가 계약 중심이며 간결한가?

## Completion Evidence

완료 선언 전 아래 3줄을 제시:

- `Primary Flow:` top-down 3~6줄
- `Boundaries:` I/O 경계 목록
- `Tests:` 계약/경계값 요약
