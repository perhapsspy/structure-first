# TypeScript Greenfield Example

[Korean](typescript.ko.md) | [English](typescript.md)


## Prompt

```text
$structure-first 를 사용해서 "알림 발송 우선순위 큐" 로직 구현해줘.
- 입력: NotificationRequest[]
- 출력: queue(정렬됨), dropped(사유 포함)
- 규칙: quiet hour 제외, severity 높은 순, 같은 severity면 createdAt 오래된 순
```

## Example Code (핵심 발췌)

```ts
export function buildNotificationQueue(input: unknown): BuildQueueResult {
  const parsed = parseNotificationRequests(input);
  if (!parsed.ok) return { ok: false, reason: 'invalid_input' };

  const split = splitDeliverable(parsed.value);
  const queue = sortByPriority(split.deliverable);

  return { ok: true, queue, dropped: split.dropped };
}

function splitDeliverable(requests: NotificationRequest[]) {
  const deliverable: NotificationRequest[] = [];
  const dropped: DroppedNotification[] = [];

  for (const req of requests) {
    const reason = validateNotification(req);
    if (reason) dropped.push({ request: req, reason });
    else deliverable.push(req);
  }

  return { deliverable, dropped };
}

function validateNotification(req: NotificationRequest): 'quiet_hour' | 'invalid_shape' | null {
  if (!req || !req.id || !req.userId) return 'invalid_shape';
  if (!Number.isFinite(req.severity) || !Number.isFinite(req.createdAt)) return 'invalid_shape';
  if (typeof req.quietHour !== 'boolean') return 'invalid_shape';
  if (req.quietHour) return 'quiet_hour';
  return null;
}
```

## Interpretation

- Primary Flow: `parse -> split -> sort`
- Boundaries: `parseNotificationRequests`
- Tests: shape/quiet hour(`validateNotification`) + 우선순위 정렬(`sortByPriority`) 계약 검증 (로컬 계약 테스트 검증됨)
