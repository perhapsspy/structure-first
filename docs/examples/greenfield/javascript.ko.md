# JavaScript Greenfield Example

[Korean](javascript.ko.md) | [English](javascript.md)


## Prompt

```text
$structure-first 로 "기능 플래그 노출 결정" 모듈 구현해줘.
- 입력: user, featureConfig
- 출력: enabled(boolean), reason
- 룰: allowlist > country block > percentage rollout
```

## Example Code (핵심 발췌)

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
- Tests: 우선순위 계약(allowlist/country/rollout) + invalid input 검증 (로컬 계약 테스트 검증됨)
