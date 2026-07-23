# Structure-First

[Korean](README.md) | [English](README.en.md)

## Summary

`structure-first` examines concrete traceability, responsibility, effect, and boundary problems exposed by a code change. It changes structure only when doing so reduces or usefully isolates total complexity; keeping the current unit is a valid result when it already supports a small coherent change.

## Quick Start

**Install**

```bash
npx skills add perhapsspy/structure-first
```

**Try It**

```text
$structure-first check whether this change exposes a concrete legibility problem
```

## When to Use

- When current behavior or decision ownership cannot be traced through a coherent path
- When effect, failure, or state ownership obscures verification
- When a short top-level flow may have displaced complexity into helpers, wrappers, context, or lifecycle

## Quick Prompt

```text
# When a structural problem is suspected
$structure-first trace this behavior in its natural reading form and improve structure only where needed

# For improving existing code
$structure-first compare the concrete structural friction with a keep-the-current-structure alternative

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
