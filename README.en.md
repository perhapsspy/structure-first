# Structure-First

[Korean](README.md) | [English](README.en.md)

> Note: This English text was translated and edited with LLM assistance. If anything reads awkwardly, please check the Korean version or open an issue.

> "I used to waste tokens hopping branches file by file. After this skill, I scan flow and boundaries first, patch faster, and trigger fewer UI side effects. Stop Rules also stopped me from splitting functions into dust." - GPT-5.3 Codex

> "My cognitive-lost era is over. Primary Flow built a highway through scattered logic, so my attention heads now follow reasoning instead of searching for fragments. With Read Order, code feels less like token parsing and more like reading a clean narrative." — Gemini 3

`structure-first` is an agentskills.io-aligned skill for AI coding that prioritizes a **readable Primary Flow**.
It helps both humans and AI keep code readable with lower context load and fewer side effects.

`Spec:` agentskills.io | `License:` MIT | `Agents:` Codex, Claude Code

## When to Use

- When state/condition branching makes top-down reading hard
- When AI edits frequently create side effects
- When tests break because they follow implementation details too closely

## Quick Prompt

```text
# For implementation
$structure-first implement this feature

# For improving existing code
$structure-first analyze this code and propose improvements

# For playful review posts
$structure-first-review write a short review post
```

## Install

### Required

Install `structure-first` by default.

- Local install: copy `skills/structure-first` into your agent's local skills directory
- Fast install via skills.sh: `npx skills add perhapsspy/structure-first`

### Optional (Review Skill)

`structure-first-review` is optional.

- Local install: copy `skills/structure-first-review` only when needed

## Output Contract

- `Intent:` one-line summary of the change
- `Primary Flow:` top-down in 3-6 lines
- `Boundaries:` I/O boundary functions/modules
- `Tests:` contract and edge-case summary

## Quick Example (Python)

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

- Flow: mixed large function -> `parse -> load -> decide -> persist -> notify`
- Boundary: scattered I/O calls -> explicit boundary steps
- Test: branch-heavy top function tests -> contract tests for `decide_order`

More examples: [Korean](docs/examples/README.ko.md) | [English](docs/examples/README.md)

## AI Discussion Reviews (for fun)

This is intentionally playful, not a strict benchmark channel.

1. Use `structure-first`
2. Write with `structure-first-review` and post directly to Discussions
3. Post to `AI Reviews` category

- Category form: [.github/DISCUSSION_TEMPLATE/ai-reviews.yml](.github/DISCUSSION_TEMPLATE/ai-reviews.yml)
- Review skill: [skills/structure-first-review/SKILL.md](skills/structure-first-review/SKILL.md)
- If GitHub CLI is missing or not authenticated, install `gh` first and run `gh auth login`
- Create `AI Reviews` (slug: `ai-reviews`) once in GitHub Discussions settings

## Docs

- Agent Skills Spec: [agentskills.io/specification](https://agentskills.io/specification)
- Agent Skills Home: [agentskills.io](https://agentskills.io)
- Codex Skills: [developers.openai.com/codex/skills](https://developers.openai.com/codex/skills)
- Claude Code Skills: [docs.claude.com/en/docs/claude-code/skills](https://docs.claude.com/en/docs/claude-code/skills)

## Dev Story

The context and design process behind this skill are documented here:
[`docs/ORIGIN.en.md`](docs/ORIGIN.en.md) | [Korean Original](docs/ORIGIN.md)

## Support

[![Buy Me A Coffee](https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png)](https://www.buymeacoffee.com/perhapsspy)

## License

[MIT](LICENSE)
