# Java Example

[Korean](java.ko.md) | [English](java.md)

> Note: This English text was translated and edited with LLM assistance. If anything reads awkwardly, please check the Korean version or open an issue.


## Problem
The service method performs validation, lookup, permission checks, state changes, notification, and events in one place, increasing regression risk on changes.

## Before

```java
public Result suspendAccount(Input input) {
    long started = System.currentTimeMillis();
    Parsed parsed = parseInput(input);
    if (!parsed.ok()) {
        audit.log("invalid_input");
        return Result.fail("invalid_input");
    }

    User actor = userRepo.find(parsed.actorId());
    Account account = accountRepo.find(parsed.accountId());
    if (actor == null || account == null) {
        audit.log("lookup_failed");
        return Result.fail("resource_not_found");
    }
    if (account.isDeleted()) {
        return Result.fail("resource_not_found");
    }

    boolean canSuspend = permission.canSuspend(actor, account);
    if (!canSuspend) {
        audit.log("forbidden", actor.id(), account.id());
        return Result.fail("forbidden");
    }

    if (account.status() == AccountStatus.SUSPENDED) {
        metrics.increment("already_suspended");
        return Result.fail("already_suspended");
    }

    if (parsed.force()) {
        audit.log("suspend_forced", actor.id(), account.id());
    }

    accountRepo.updateStatus(account.id(), AccountStatus.SUSPENDED);
    accountRepo.touchUpdatedAt(account.id());
    if (parsed.clearSessions()) {
        sessionRepo.revokeAll(account.userId());
    }

    if (parsed.notifyOwner()) {
        try {
            notifier.send(account.ownerEmail(), "account_suspended");
            if (parsed.notifyActor()) {
                notifier.send(actor.email(), "suspend_done");
            }
        } catch (Exception e) {
            audit.log("notify_failed", account.id());
        }
    }

    try {
        eventBus.publish("account.suspended", account.id(), actor.id());
    } catch (Exception e) {
        audit.log("event_publish_failed", account.id());
    }
    metrics.increment("account_suspended");
    metrics.timing("suspend_account_ms", System.currentTimeMillis() - started);

    return Result.ok(account.id());
}
```

## After (Applied with structure-first)

```java
public Result suspendAccount(Input input) {
    var req = parseSuspendRequest(input);
    if (req.isFail()) return Result.fail("invalid_input");

    var ctx = loadSuspendContext(req.value());
    if (ctx.isFail()) return Result.fail(ctx.reason());

    var decision = decideSuspend(ctx.value());
    if (decision.isFail()) return Result.fail(decision.reason());

    var saved = persistSuspend(decision.value());
    notifySuspend(saved, req.value());
    publishSuspended(saved.accountId(), saved.actorId());
    recordSuspendMetrics(saved.startedAt());

    return Result.ok(saved.accountId());
}

DecisionResult decideSuspend(SuspendContext ctx) {
    if (!ctx.permission().canSuspend()) return DecisionResult.fail("forbidden");
    if (ctx.account().status() == AccountStatus.SUSPENDED) return DecisionResult.fail("already_suspended");
    if (ctx.account().isDeleted()) return DecisionResult.fail("resource_not_found");
    return DecisionResult.ok(new SuspendDecision(ctx.account().id(), ctx.actor().id(), ctx.request().clearSessions()));
}
```

## Interpretation

- Primary Flow: `parse -> load -> decide -> persist -> notify -> publish -> metrics`
- Boundary(I/O): `loadSuspendContext`, `persistSuspend`, `notifySuspend`, `publishSuspended`, `recordSuspendMetrics`
- Atom(domain): `decideSuspend`
- Readability impact: the service method keeps only flow orchestration while policy decisions are fixed by the `decideSuspend` contract.
