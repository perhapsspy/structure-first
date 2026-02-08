# JavaScript Greenfield Example

[Korean](javascript.ko.md) | [English](javascript.md)

> Note: This English text was translated and edited with LLM assistance. If anything reads awkwardly, please check the Korean version or open an issue.


## Prompt

```text
$structure-first implement a "feature exposure decision" module.
- Input: user, featureConfig
- Output: enabled (boolean), reason
- Rule: allowlist > country block > percentage rollout
```

## Example Code (Core Excerpt)

```js
export function decideFeatureExposure(input) {
  const ctxResult = buildExposureContext(input);
  if (!ctxResult.ok) return fail(ctxResult.reason);

  const decision = decideExposure(ctxResult.value);
  if (!decision.ok) return fail(decision.reason);

  return { ok: true, enabled: decision.value.enabled, reason: decision.value.reason };
}

function decideExposure(ctx) {
  if (isAllowlisted(ctx.userId, ctx.allowlist)) {
    return ok({ enabled: true, reason: 'allowlist' });
  }
  if (isBlockedCountry(ctx.country, ctx.blockedCountries)) {
    return ok({ enabled: false, reason: 'country_block' });
  }
  return ok({ enabled: inRollout(ctx.userId, ctx.rolloutPercent), reason: 'percentage_rollout' });
}
```

## Interpretation

- Primary Flow: `build context -> decide`
- Boundaries: `buildExposureContext`
- Tests: priority contracts (allowlist/country/rollout) + invalid input checks (verified with local contract tests)
