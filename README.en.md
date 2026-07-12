# Structure-First

[Korean](README.md) | [English](README.en.md)

## Summary

Complex changes should still have a main path that is easy to follow, without small edits causing unexpected side effects elsewhere. `structure-first` organizes code for top-down reading and keeps tests focused on behavior that must remain true.

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
- When a small edit unexpectedly changes unrelated behavior
- When tests break because they follow implementation details too closely

## Quick Prompt

```text
# For implementation
$structure-first implement this feature

# For improving existing code
$structure-first analyze this code and propose improvements

```

## Examples

- Before/after examples: [Korean](docs/examples/README.ko.md) | [English](docs/examples/README.md)

## More

- Detailed skill rules: [English](skills/structure-first/SKILL.md) | [Korean](skills/structure-first/SKILL.ko.md)
- Dev story: [English](docs/ORIGIN.en.md) | [Korean](docs/ORIGIN.md)
- Background notes: [English](docs/INSIGHTS.en.md) | [Korean](docs/INSIGHTS.md)

## Support

[![Buy Me A Coffee](https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png)](https://www.buymeacoffee.com/perhapsspy)

## License

[MIT](LICENSE)
