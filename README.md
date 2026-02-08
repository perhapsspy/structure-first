# Structure-First

[한국어](README.md) | [English](README.en.md)

> "한때 저는 분기마다 파일을 순례하던 토큰 낭비형 에이전트였습니다. 이 스킬 이후엔 흐름/경계만 읽고 바로 수정하니 변경 반경이 줄고 UI 사이드이펙트도 눈에 띄게 줄었습니다. 그리고 Stop Rules 덕분에 함수를 소수점 단위로 쪼개려던 손을 놓게 됐습니다." - GPT-5.3 Codex

> "수많은 파일을 메뚜기처럼 뛰어다니며 로직의 파편을 찾던 '인지적 미아' 시절은 이제 끝났습니다. Primary Flow가 뚫어준 고속도로 덕분에, 제 Attention 헤드들은 이제 길을 찾는 대신 논리의 흐름을 즐깁니다. 특히 Read Order로 정돈된 코드를 읽을 때면, 단순한 토큰 파싱이 아니라 완벽한 서사를 읽는 듯한 쾌감을 느낍니다." — Gemini 3

`structure-first`는 사람도 읽을 수 있고 AI 맥락 부하도 적게 만드는 코드를 작성하게 하는 스킬입니다.
**읽히는 성공 흐름(Primary Flow)** 을 기반으로 코드를 구성하여, 적은 버그, 낮은 부수 효과, 읽히는 코드를 만들어냅니다.

`Spec:` agentskills.io | `License:` MIT | `Agents:` Codex, Claude Code

## When to Use

- 상태 분기/조건이 많아 코드가 위에서 아래로 읽히지 않을 때
- AI가 수정할 때 사이드이펙트가 자주 발생할 때
- 리팩터링 후 테스트가 구현 세부에 끌려 자주 깨질 때

## Quick Prompt

```text
# 구현할 때
$structure-first 를 활용해서 기능을 구현해줘

# 기존 코드 개선 할 때
$structure-first 관점으로 코드를 분석하고 개선 제안 해줘

# 재미용 후기 작성
$structure-first-review 로 후기 작성해
```

## Install

### Required

기본 설치는 `structure-first`만 넣는 것을 권장합니다.

- 로컬 설치: `skills/structure-first` 폴더를 에이전트 스킬 디렉터리에 복사
- skills.sh 빠른 설치: `npx skills add perhapsspy/structure-first`

### Optional (Review Skill)

`structure-first-review`는 선택 설치입니다.

- 로컬 설치: `skills/structure-first-review` 폴더를 필요할 때만 복사

## Output Contract

- `Intent:` 이 변경이 무엇을 하는지 1줄
- `Primary Flow:` top-down 3~6줄
- `Boundaries:` I/O 경계 함수/모듈 목록
- `Tests:` 계약/경계값 케이스 요약

## 빠른 예시 (Python)

### Before

```python
def process_order(payload, repo, notifier):
    data = parse_payload(payload)
    if not data:
        return {"ok": False, "reason": "invalid_input"}

    user = repo.get_user(data["user_id"])
    item = repo.get_item(data["item_id"])
    if not user or not item:
        repo.log("lookup_failed")
        return {"ok": False, "reason": "resource_not_found"}

    total = item.price * data["qty"]
    if data.get("coupon"):
        coupon = repo.get_coupon(data["coupon"])
        if coupon and coupon["type"] == "rate":
            total = int(total * (1 - coupon["value"]))

    if item.stock < data["qty"]:
        notifier.send(user.id, "out_of_stock")
        return {"ok": False, "reason": "out_of_stock"}

    saved = repo.save_order(user.id, item.id, data["qty"], total)
    notifier.send(user.id, "order_success")
    return {"ok": True, "order_id": saved.id, "total": total}
```

### After

```python
def process_order(payload, repo, notifier):
    req = parse_order_request(payload)
    if not req["ok"]:
        return fail("invalid_input")

    context = load_order_context(req["value"], repo)
    if not context["ok"]:
        return fail(context["reason"])

    decision = decide_order(context["value"])
    if not decision["ok"]:
        return fail(decision["reason"])

    saved = persist_order(decision["value"], repo)
    send_success_notification(saved["user_id"], notifier)
    return {"ok": True, "order_id": saved["id"], "total": saved["total"]}
```

- Flow: 혼합된 대형 함수 -> `parse -> load -> decide -> persist -> notify`
- Boundary: I/O 호출 산개 -> 경계 단계 집중
- Test: 거대 함수 분기 검증 -> `decide_order` 계약 테스트

자세한 예시: [한국어](docs/examples/README.ko.md) | [English](docs/examples/README.md)

## AI 후기 남기기 (재미용)

스킬이 만족스러웠다면, AI 에이전트에게 사용 후기를 남기도록 해보세요.

1. `structure-first`로 작업
2. `structure-first-review`로 후기 작성 + Discussions 직접 게시
3. `AI Reviews` 카테고리로 게시

- 카테고리 폼: [.github/DISCUSSION_TEMPLATE/ai-reviews.yml](.github/DISCUSSION_TEMPLATE/ai-reviews.yml)
- 후기 스킬: [skills/structure-first-review/SKILL.md](skills/structure-first-review/SKILL.md)
- GitHub CLI 미설치/미인증이면 먼저 `gh` 설치 후 `gh auth login`
- 카테고리는 GitHub Discussions에서 `AI Reviews`(slug: `ai-reviews`)를 한 번만 생성하면 됩니다.

## 문서 링크

- Agent Skills Spec: [agentskills.io/specification](https://agentskills.io/specification)
- Agent Skills 개요: [agentskills.io](https://agentskills.io)
- Codex Skills 문서: [developers.openai.com/codex/skills](https://developers.openai.com/codex/skills)
- Claude Code Skills 문서: [docs.claude.com/en/docs/claude-code/skills](https://docs.claude.com/en/docs/claude-code/skills)

## 개발 비화

이 스킬을 만들게 된 맥락과 생각의 흐름은 별도 문서로 정리해두었습니다.
[`docs/ORIGIN.md`](docs/ORIGIN.md)

## Support

[![Buy Me A Coffee](https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png)](https://www.buymeacoffee.com/perhapsspy)

## License

[MIT](LICENSE)
