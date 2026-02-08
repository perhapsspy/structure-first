# Java Greenfield Example

[Korean](java.ko.md) | [English](java.md)

> Note: This English text was translated and edited with LLM assistance. If anything reads awkwardly, please check the Korean version or open an issue.


## Prompt

```text
$structure-first implement a "leave request approval workflow".
- Input: requestId, approverId
- Rule: load request -> decide approval -> change status -> notify
- Keep failure reasons fixed
```

## Example Code (Core Excerpt)

```java
public Result approveLeave(String requestId, String approverId) {
    var context = loadLeaveApprovalContext(requestId, approverId);
    if (context.isFail()) return Result.fail(context.reason());

    var decision = decideLeaveApproval(context.value());
    if (decision.isFail()) return Result.fail(decision.reason());

    var saved = persistLeaveApproval(decision.value());
    notifyLeaveApproved(saved.requesterId(), saved.requestId());

    return Result.ok(saved.requestId());
}

DecisionResult decideLeaveApproval(LeaveApprovalContext ctx) {
    if (!ctx.permission().canApprove()) return DecisionResult.fail("forbidden");
    if (ctx.request().status() != LeaveStatus.PENDING) return DecisionResult.fail("not_pending");
    if (ctx.request().days() > ctx.policy().maxDays()) return DecisionResult.fail("exceeds_policy");

    return DecisionResult.ok(new LeaveApprovalDecision(
        ctx.request().id(),
        ctx.approver().id(),
        LeaveStatus.APPROVED
    ));
}
```

## Interpretation

- Primary Flow: `load -> decide -> persist -> notify`
- Boundaries: `loadLeaveApprovalContext`, `persistLeaveApproval`, `notifyLeaveApproved`
- Tests: success/input contracts for `approveLeave` + forbidden contract for `decideLeaveApproval` (verified with local contract tests)
