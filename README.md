# Structure-First

[한국어](README.md) | [English](README.en.md)

## 요약

`structure-first`는 기능 구현, 버그 수정과 리팩터링에서 동작의 흐름이 자연스럽게 읽히고, 책임이 분명한 지점에서 조합되며, 부작용과 상태의 경계가 드러나도록 코드를 다룹니다. 바뀐 동작은 구현 세부가 아니라 계약 중심 테스트로 검증합니다.

## 빠른 시작

**설치**

```bash
npx skills add perhapsspy/structure-first
```

**바로 사용**

```text
$structure-first 로 이 기능을 읽고 고치기 쉬운 흐름과 책임으로 구현해줘
```

## 이런 때 사용

- 기능 구현, 버그 수정이나 리팩터링에서 코드 흐름과 책임을 함께 다룰 때
- 조합, 부작용·실패 의미나 상태 소유권을 분명하게 해야 할 때
- 구조를 단순하게 유지하면서 바뀐 동작을 계약 중심으로 검증할 때

## 프롬프트 예시

```text
# 기능이나 동작을 변경할 때
$structure-first 로 동작을 자연스럽게 읽히게 구현하고, 구조는 필요한 만큼만 바꿔줘

# 기존 코드 개선 할 때
$structure-first 관점으로 실제로 읽고 고치기 어려운 지점과 기존 구조를 유지하는 방향을 함께 비교해줘

```

## 예시

- 전후 비교 예시: [한국어](docs/examples/README.ko.md) | [English](docs/examples/README.md)

## 더 보기

- 스킬 상세 규칙: [한국어](skills/structure-first/SKILL.ko.md) | [English](skills/structure-first/SKILL.md)
- 개발 배경: [한국어](docs/ORIGIN.md) | [English](docs/ORIGIN.en.md)
- 배경 메모: [한국어](docs/INSIGHTS.md) | [English](docs/INSIGHTS.en.md)

## 지원

[![Buy Me A Coffee](https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png)](https://www.buymeacoffee.com/perhapsspy)

## 라이선스

[MIT](LICENSE)
