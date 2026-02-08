# Go Example

[Korean](go.ko.md) | [English](go.md)


## Problem
체크아웃 핸들러에서 요청 파싱, 조회, 정책 판단, 결제 승인, 저장, 이벤트 발행까지 모두 처리해 장애 원인 분리가 어려운 상태.

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
- 읽기 기준 변화: 핸들러에서 정책 계산을 분리해 결제/저장 장애와 정책 변경을 독립적으로 다룰 수 있다.
