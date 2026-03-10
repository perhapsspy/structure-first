# Structure-First

[Korean](README.md) | [English](README.en.md)

> Note: This English text was translated and edited with LLM assistance. If anything reads awkwardly, please check the Korean version or open an issue.

## Summary

`structure-first` is a skill for making the **Primary Flow** of code readable first.
It keeps boundaries minimal, pushes detail downward, and favors contract-focused tests.
The goal is to reduce change radius and side effects during complex changes.

`Spec:` agentskills.io | `License:` MIT | `Agents:` Codex, Claude Code

The optional `structure-first-docs` skill applies the same philosophy to engineering documents such as design docs, plans, and runbooks.

## Quick Start

**Install**

```bash
npx skills add perhapsspy/structure-first
```

**Try It**

```text
$structure-first implement this feature
```

## When to Use

- When state/condition branching makes top-down reading hard
- When AI edits frequently create side effects
- When tests break because they follow implementation details too closely

## Install

### Required

Start with `structure-first` first, then add companion skills only when needed.

- Fast install via skills.sh: `npx skills add perhapsspy/structure-first`
- Local install: copy `skills/structure-first` into your agent's local skills directory

### Optional

- `structure-first-review`: optional skill for writing/posting playful reviews
- `structure-first-docs`: optional companion skill that applies the same structural philosophy to document writing/review

## Quick Prompt

```text
# For implementation
$structure-first implement this feature

# For improving existing code
$structure-first analyze this code and propose improvements

# To apply the same philosophy to docs
$structure-first-docs write/review this design doc

# For playful review posts
$structure-first-review write a short review post
```

## Examples

- Before/after examples: [Korean](docs/examples/README.ko.md) | [English](docs/examples/README.md)

## More

- Detailed skill rules: [English](skills/structure-first/SKILL.md) | [Korean](skills/structure-first/SKILL.ko.md)
- Docs companion skill: [English](skills/structure-first-docs/SKILL.md) | [Korean](skills/structure-first-docs/SKILL.ko.md)
- Dev story: [English](docs/ORIGIN.en.md) | [Korean](docs/ORIGIN.md)
- Background notes: [English](docs/INSIGHTS.en.md) | [Korean](docs/INSIGHTS.md)

## Support

[![Buy Me A Coffee](https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png)](https://www.buymeacoffee.com/perhapsspy)

## License

[MIT](LICENSE)
