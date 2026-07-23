# Structure-First

[한국어](README.md) | [English](README.en.md)

## 요약

코드 변경에서 실제로 드러난 추적·책임·부작용·경계 문제를 살펴보고, 구조를 바꾸는 편이 전체 복잡도를 줄일 때만 손봅니다. 기존 단위가 작은 일관된 변경을 이미 수용한다면 그대로 두는 것도 정상적인 결과입니다.

## 빠른 시작

**설치**

```bash
npx skills add perhapsspy/structure-first
```

**바로 사용**

```text
$structure-first 로 이 변경에서 추적하기 어려운 구조 문제가 있는지 살펴봐줘
```

## 이런 때 사용

- 현재 동작이나 결정 책임을 한 경로로 추적하기 어려울 때
- 부작용·실패 의미·상태 소유권이 변경 검증을 흐릴 때
- 짧아진 상위 흐름 아래 helper, wrapper, context, lifecycle이 늘어 복잡도가 이동했는지 확인할 때

## 프롬프트 예시

```text
# 구조 문제가 의심될 때
$structure-first 로 현재 동작을 자연스러운 읽기 형태로 추적하고, 필요한 만큼만 구조를 개선해줘

# 기존 코드 개선 할 때
$structure-first 관점으로 구체적인 구조 마찰과 구조를 유지하는 대안까지 비교해줘

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
