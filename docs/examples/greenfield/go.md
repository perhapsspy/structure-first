# Go Greenfield Example

[Korean](go.ko.md) | [English](go.md)

> Note: This English text was translated and edited with LLM assistance. If anything reads awkwardly, please check the Korean version or open an issue.


## Prompt

```text
$structure-first implement a "webhook signature verification + idempotency" handler.
- Input: Request
- Rule: verify signature -> check idempotency key -> persist event
- If duplicate, return success
```

## Example Code (Core Excerpt)

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
- Tests: contract checks for `DecideWebhook` + idempotency re-request/event persistence in `HandleWebhook` (verified with local contract tests)
