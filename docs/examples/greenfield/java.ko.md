# Java Greenfield Example

[Korean](java.ko.md) | [English](java.md)


## Prompt

```text
$structure-first 를 써서 "휴가 요청 승인 워크플로" 구현해줘.
- 입력: requestId, approverId
- 규칙: 요청 조회 -> 승인 가능 여부 판단 -> 상태 변경 -> 알림
- 실패 reason 고정
```

## Example Code (핵심 발췌)

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
- Tests: `approveLeave` 성공/입력 검증 + `decideLeaveApproval` forbidden 계약 검증 (로컬 계약 테스트 검증됨)
