# Rust Example

[Korean](rust.ko.md) | [English](rust.md)

> Note: This English text was translated and edited with LLM assistance. If anything reads awkwardly, please check the Korean version or open an issue.


## Problem
Stock reservation mixes parsing, lookup, policy decisions, persistence, and event publishing; `Result` exists but responsibility boundaries are unclear.

## Before

```rust
pub async fn reserve_stock(input: Value, deps: &Deps) -> Result<Output, ErrorReason> {
    let started = std::time::Instant::now();
    let req = match parse_input(input) {
        Some(v) => v,
        None => {
            deps.audit.log("invalid_input").await.ok();
            return Err(ErrorReason::InvalidInput);
        }
    };

    let item = deps.item_repo.find(req.item_id).await.ok_or(ErrorReason::ItemNotFound)?;
    let warehouse = deps
        .wh_repo
        .find(req.warehouse_id)
        .await
        .ok_or(ErrorReason::WarehouseNotFound)?;
    if warehouse.disabled {
        return Err(ErrorReason::WarehouseNotFound);
    }

    if item.disabled || !warehouse.active {
        deps.audit.log("reserve_unavailable").await.ok();
        return Err(ErrorReason::Unavailable);
    }

    let mut qty = req.qty;
    if let Some(limit) = warehouse.policy.max_reserve {
        if qty > limit {
            qty = limit;
        }
    }

    if item.stock < qty {
        deps.notify.send(req.user_id, "out_of_stock").await.ok();
        return Err(ErrorReason::OutOfStock);
    }
    if req.expedite {
        qty = qty.min(item.stock);
    }

    let hold = deps.hold_repo.save(item.id, qty).await?;
    if req.clear_cart {
        deps.cart_repo.clear(req.cart_id).await.ok();
    }

    if let Err(e) = deps.event_bus.publish("stock.reserved", hold.id).await {
        deps.audit.log(format!("publish_failed:{e}")).await.ok();
    }
    deps.metrics
        .timing("reserve_stock_ms", started.elapsed().as_millis() as u64)
        .await
        .ok();

    Ok(Output { hold_id: hold.id })
}
```

## After (Applied with structure-first)

```rust
pub async fn reserve_stock(input: Value, deps: &Deps) -> Result<Output, ErrorReason> {
    let req = parse_reserve_request(input)?;
    let ctx = load_reserve_context(&req, deps).await?;
    let decision = decide_reserve(&ctx)?;
    let saved = persist_reserve(&decision, deps).await?;
    publish_stock_reserved(saved.hold_id, deps).await?;
    record_reserve_metrics(ctx.started_at, deps).await;
    Ok(Output { hold_id: saved.hold_id })
}

fn decide_reserve(ctx: &ReserveContext) -> Result<ReserveDecision, ErrorReason> {
    let qty = apply_reserve_limit(ctx.request.qty, ctx.warehouse.policy.max_reserve);

    if ctx.item.disabled || !ctx.warehouse.active {
        return Err(ErrorReason::Unavailable);
    }
    if ctx.item.stock < qty {
        return Err(ErrorReason::OutOfStock);
    }

    Ok(ReserveDecision {
        item_id: ctx.item.id,
        qty,
        clear_cart: ctx.request.clear_cart,
        cart_id: ctx.request.cart_id,
    })
}
```

## Interpretation

- Primary Flow: `parse -> load -> decide -> persist -> publish -> metrics`
- Boundary(I/O): `load_reserve_context`, `persist_reserve`, `publish_stock_reserved`, `record_reserve_metrics`
- Atom(domain): `apply_reserve_limit`, `decide_reserve`
- Readability impact: async I/O and stock policy decisions are separated, making stage-by-stage error tracing easier.
