# Go Example

[Korean](go.ko.md) | [English](go.md)

> Note: This English text was translated and edited with LLM assistance. If anything reads awkwardly, please check the Korean version or open an issue.


## Problem
The checkout handler mixes parsing, lookup, policy decisions, payment approval, persistence, and event publishing, making failure isolation difficult.

## Before

```go
func HandleCheckout(w http.ResponseWriter, r *http.Request, deps Deps) {
	started := time.Now()
	req, ok := ParseCheckoutRequest(r)
	if !ok {
		deps.Logger.Warn("invalid_input")
		WriteFail(w, "invalid_input")
		return
	}

	user, userOK := deps.UserRepo.Find(req.UserID)
	cart, cartOK := deps.CartRepo.Find(req.CartID)
	if !userOK || !cartOK {
		deps.Audit.Log("checkout_lookup_failed", map[string]any{"user": userOK, "cart": cartOK})
		WriteFail(w, "resource_not_found")
		return
	}
	if cart.Archived {
		WriteFail(w, "resource_not_found")
		return
	}

	if !CanCheckout(user, cart) {
		deps.Audit.Log("checkout_forbidden", map[string]any{"userId": user.ID, "cartId": cart.ID})
		WriteFail(w, "forbidden")
		return
	}

	amount := cart.Total
	if req.CouponCode != "" {
		coupon, found := deps.CouponRepo.Find(req.CouponCode)
		if found {
			if coupon.Type == "RATE" {
				amount = int(float64(amount) * (1 - coupon.Value))
			} else if coupon.Type == "AMOUNT" {
				amount = amount - coupon.Value
				if amount < 0 {
					amount = 0
				}
			}
		}
	}
	if req.Expedite {
		amount += 300
	}
	if req.PointsToUse > 0 {
		amount = amount - req.PointsToUse
		if amount < 0 {
			amount = 0
		}
	}

	var approved PaymentResult
	for i := 0; i < 2; i++ {
		approved = deps.PaymentAPI.Approve(req.PaymentToken, amount)
		if approved.OK {
			break
		}
		deps.Logger.Info("payment_retry", map[string]any{"attempt": i + 1, "userId": user.ID})
	}
	if !approved.OK {
		deps.Logger.Info("payment_failed", map[string]any{"userId": user.ID, "amount": amount, "cartId": cart.ID})
		WriteFail(w, "payment_failed")
		return
	}

	saved := deps.OrderRepo.Save(user.ID, cart.ID, amount, approved.TxID)
	if req.ClearCart {
		deps.CartRepo.Clear(cart.ID)
	}
	if err := deps.EventBus.Publish("order.created", saved.ID); err != nil {
		deps.Logger.Warn("publish_failed", map[string]any{"orderId": saved.ID})
	}
	if deps.Metrics != nil {
		deps.Metrics.Histogram("checkout.duration_ms", time.Since(started).Milliseconds(), map[string]string{
			"userTier": user.Tier,
		})
	}

	WriteSuccess(w, saved.ID)
}
```

## After (Applied with structure-first)

```go
func HandleCheckout(w http.ResponseWriter, r *http.Request, deps Deps) {
	request, ok := ParseCheckoutRequest(r)
	if !ok {
		WriteFail(w, "invalid_input")
		return
	}

	context, err := LoadCheckoutContext(request, deps)
	if err != nil {
		WriteFail(w, err.Reason)
		return
	}

	decision, err := DecideCheckout(context)
	if err != nil {
		WriteFail(w, err.Reason)
		return
	}

	saved, err := PersistCheckout(decision, deps)
	if err != nil {
		WriteFail(w, err.Reason)
		return
	}

	PublishOrderCreated(saved.ID, deps)
	RecordCheckoutMetrics(context.StartedAt, context.User.Tier, deps)
	WriteSuccess(w, saved.ID)
}

func DecideCheckout(ctx CheckoutContext) (CheckoutDecision, *DomainError) {
	amount := ApplyCoupon(ctx.Cart.Total, ctx.Coupon)
	amount = ApplyExpediteFee(amount, ctx.Request.Expedite)
	amount = ApplyPoints(amount, ctx.Request.PointsToUse)
	if amount < 0 {
		return CheckoutDecision{}, &DomainError{Reason: "invalid_amount"}
	}
	return CheckoutDecision{UserID: ctx.User.ID, CartID: ctx.Cart.ID, Amount: amount, ClearCart: ctx.Request.ClearCart}, nil
}
```

## Interpretation

- Primary Flow: `parse -> load -> decide -> persist -> publish -> metrics -> respond`
- Boundary(I/O): `LoadCheckoutContext`, `PersistCheckout`, `PublishOrderCreated`, `RecordCheckoutMetrics`
- Atom(domain): `ApplyCoupon`, `ApplyExpediteFee`, `ApplyPoints`, `DecideCheckout`
- Readability impact: policy calculation is separated from the handler, so payment/persistence failures and policy changes can be handled independently.
