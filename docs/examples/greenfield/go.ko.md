# Go Greenfield Example

[Korean](go.ko.md) | [English](go.md)


## Prompt

```text
$structure-first 로 "웹훅 서명 검증 + 중복 처리" 핸들러 구현해줘.
- 입력: Request
- 규칙: signature 검증 -> idempotency key 확인 -> 이벤트 저장
- 중복이면 성공 반환
```

## Example Code (핵심 발췌)

```go
func HandleWebhook(req Request, deps Deps) map[string]any {
	ctx, err := LoadWebhookContext(req, deps)
	if err != nil {
		return fail(err.Reason)
	}

	decision, err := DecideWebhook(ctx)
	if err != nil {
		return fail(err.Reason)
	}

	if decision.Duplicate {
		return map[string]any{"ok": true, "duplicate": true}
	}

	if err := PersistWebhookEvent(decision, deps); err != nil {
		return fail(err.Reason)
	}

	return map[string]any{"ok": true, "duplicate": false}
}

func DecideWebhook(ctx Context) (Decision, *DomainError) {
	if !VerifySignature(ctx.Request.RawBody, ctx.Request.Signature, ctx.Secret) {
		return Decision{}, &DomainError{Reason: "invalid_signature"}
	}
	if ctx.IdempotencyExists {
		return Decision{Duplicate: true, EventID: ctx.Request.EventID, IdempotencyKey: ctx.Request.IdempotencyKey}, nil
	}
	return Decision{Duplicate: false, EventID: ctx.Request.EventID, IdempotencyKey: ctx.Request.IdempotencyKey}, nil
}
```

## Interpretation

- Primary Flow: `load -> decide -> persist`
- Boundaries: `LoadWebhookContext`, `PersistWebhookEvent`
- Tests: `DecideWebhook` 계약 + `HandleWebhook` idempotency key 재요청/이벤트 저장 계약 검증 (로컬 계약 테스트 검증됨)
