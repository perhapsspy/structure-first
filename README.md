# Structure-First

[한국어](README.md) | [English](README.en.md)

## Summary

`structure-first`는 코드의 **성공 흐름(Primary Flow)** 을 먼저 읽히게 정리하는 스킬입니다.
경계는 필요한 만큼만 두고, 세부는 아래로 내리며, 테스트는 계약 중심으로 맞춥니다.
복잡한 변경에서도 변경 반경과 부수 효과를 줄이는 데 초점을 둡니다.

`Spec:` agentskills.io | `License:` MIT | `Agents:` Codex, Claude Code

선택 스킬인 `structure-first-docs`는 같은 철학을 설계 문서, 계획 문서, 런북 같은 엔지니어링 문서에 적용합니다.

## Quick Start

**설치**

```bash
npx skills add perhapsspy/structure-first
```

**바로 사용**

```text
$structure-first 를 활용해서 기능을 구현해줘
```

## When to Use

- 상태 분기/조건이 많아 코드가 위에서 아래로 읽히지 않을 때
- AI가 수정할 때 사이드이펙트가 자주 발생할 때
- 리팩터링 후 테스트가 구현 세부에 끌려 자주 깨질 때

## Install

### Required

기본 경로는 `structure-first`부터 시작하고, companion skill은 필요할 때만 추가하는 방식입니다.

- skills.sh 빠른 설치: `npx skills add perhapsspy/structure-first`
- 로컬 설치: `skills/structure-first` 폴더를 에이전트 스킬 디렉터리에 복사

### Optional

- `structure-first-review`: 후기 작성/게시용 선택 스킬
- `structure-first-docs`: 같은 구조 철학을 문서 작성/리뷰에 적용하는 companion 스킬

## Quick Prompt

```text
# 구현할 때
$structure-first 를 활용해서 기능을 구현해줘

# 기존 코드 개선 할 때
$structure-first 관점으로 코드를 분석하고 개선 제안 해줘

# 같은 철학을 문서에 적용할 때
$structure-first-docs 관점으로 설계 문서를 작성/리뷰 해줘

# 재미용 후기 작성
$structure-first-review 로 후기 작성해
```

## Examples

- Before/after examples: [한국어](docs/examples/README.ko.md) | [English](docs/examples/README.md)

## More

- Detailed skill rules: [한국어](skills/structure-first/SKILL.ko.md) | [English](skills/structure-first/SKILL.md)
- Docs companion skill: [한국어](skills/structure-first-docs/SKILL.ko.md) | [English](skills/structure-first-docs/SKILL.md)
- Dev story: [한국어](docs/ORIGIN.md) | [English](docs/ORIGIN.en.md)
- Background notes: [한국어](docs/INSIGHTS.md) | [English](docs/INSIGHTS.en.md)

## Support

[![Buy Me A Coffee](https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png)](https://www.buymeacoffee.com/perhapsspy)

## License

[MIT](LICENSE)
