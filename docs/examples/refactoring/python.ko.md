# Python Example

[Korean](python.ko.md) | [English](python.md)


## Problem
구독 결제 함수 하나에 조회/정책계산/결제/저장/알림이 몰려 있어, 작은 정책 변경도 회귀 위험이 큰 상태.

## Before

```python
def charge_subscription(user_id, plan_code, token, deps, coupon_code=None, trial=False):
    user = deps.user_repo.get(user_id)
    if not user:
        return {"ok": False, "reason": "invalid_user"}
    if not user.active:
        return {"ok": False, "reason": "inactive_user"}

    plan = deps.plan_repo.get(plan_code)
    if not plan:
        deps.logger.info("plan_missing", {"plan": plan_code})
        return {"ok": False, "reason": "plan_not_found"}

    amount = plan.monthly_price

    # 정책이 매번 덧붙는 스타일
    if trial:
        amount = 0
    if user.segment == "enterprise":
        amount = int(amount * 0.95)
    if coupon_code:
        coupon = deps.coupon_repo.get(coupon_code)
        if coupon:
            if coupon.get("type") == "rate":
                amount = int(amount * (1 - coupon.get("value", 0)))
            elif coupon.get("type") == "amount":
                amount = amount - coupon.get("value", 0)
            elif coupon.get("type") == "free_trial":
                amount = 0
    if amount < 0:
        amount = 0

    country = (user.country or "US").upper()
    if country == "KR":
        amount = int(round(amount * 1.1))
    elif country == "JP":
        amount = int(round(amount * 1.1))
    elif country == "DE":
        amount = int(round(amount * 1.19))
    if plan.currency != "USD":
        rate = deps.fx.get_rate(plan.currency, "USD")
        if rate:
            amount = int(round(amount * rate))

    paid = None
    if amount == 0:
        tx_id = "TRIAL"
    else:
        for attempt in range(2):
            paid = deps.payment_gateway.charge(token, amount)
            if paid and paid.get("ok"):
                break
            deps.logger.info("charge_retry", {"user": user.id, "attempt": attempt + 1})
        if not paid or not paid.get("ok"):
            deps.logger.warn("payment_failed", {"user": user.id, "amount": amount, "plan": plan_code})
            return {"ok": False, "reason": "payment_failed"}
        tx_id = paid.get("tx_id")

    invoice = deps.invoice_repo.save(user.id, plan.code, amount, tx_id)

    try:
        deps.mailer.send(user.email, "billing_success")
    except Exception:
        deps.logger.warn("mail_failed", {"user": user.id})

    event = "trial_started" if trial or amount == 0 else "subscription_charged"
    deps.analytics.track(event, {"user": user.id, "plan": plan.code, "amount": amount})

    return {"ok": True, "invoice_id": invoice.id, "amount": amount}
```

## After (Applied with structure-first)

```python
def charge_subscription(user_id, plan_code, token, deps, coupon_code=None, trial=False):
    req = build_charge_request(user_id, plan_code, token, coupon_code, trial)

    context_result = load_charge_context(req, deps)
    if not context_result["ok"]:
        return fail(context_result["reason"])

    decision_result = decide_charge(context_result["value"])
    if not decision_result["ok"]:
        return fail(decision_result["reason"])

    payment_result = execute_payment(decision_result["value"], token, deps)
    if not payment_result["ok"]:
        return fail(payment_result["reason"])

    saved = persist_invoice(context_result["value"], decision_result["value"], payment_result["tx_id"], deps)
    send_billing_success(context_result["value"].user.email, deps)
    track_charge_event(context_result["value"], saved.amount, deps)

    return {"ok": True, "invoice_id": saved.id, "amount": saved.amount}


def decide_charge(ctx):
    amount = apply_trial_rule(ctx.plan_monthly, ctx.request.trial)
    amount = apply_segment_discount(amount, ctx.user.segment)
    amount = apply_coupon(amount, ctx.coupon)
    amount = apply_country_tax(amount, ctx.user.country)
    amount = apply_currency_conversion(amount, ctx.plan_currency, ctx.fx_rate)

    if amount < 0:
        return fail("invalid_amount")

    return {"ok": True, "value": {"amount": amount, "currency": "USD"}}
```

## Interpretation

- Primary Flow: `build request -> load -> decide -> pay -> persist -> notify -> track`
- Boundary(I/O): `load_charge_context`, `execute_payment`, `persist_invoice`, `send_billing_success`, `track_charge_event`
- Atom(domain): `apply_trial_rule`, `apply_segment_discount`, `apply_coupon`, `apply_country_tax`, `apply_currency_conversion`, `decide_charge`
- 읽기 기준 변화: 금액 계산 정책을 atom으로 고정해 규칙 변경과 I/O 변경을 분리할 수 있다.
